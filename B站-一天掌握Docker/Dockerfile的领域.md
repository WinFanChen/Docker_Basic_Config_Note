## Dockerfile指令
docker image build 命令通过 dockerfile 文件来构建镜像

* dockerfile文件示例
```
from centos:7
maintainer www.aliangedu.com
run yum install...                      //构建镜像时运行shell命令
cmd ["./sbin/php-ftp","-c",...]         //运行镜像时运行shell命令 用数组实现 一般用来启脚本什么的
expose 80                               //声明端口
env java_home /usr/lcoal/jdk1.8.0_45    //声明容器内环境变量java_home
add php-5.6.31.tar.gz /tmp/             //拷贝文件/目录到镜像 不建议使用url 压缩包会自动解压
copy                                    //无解压功能的add
entrypoint                              //在使用docker run [options] image [command] 时接收command
volume                                  //还记得在run时的挂载吗? 这个不常用
user root                               //使用 root 用户权限执行run,cmd,entrypoint命令
workdir /data                           //设定run,cmd,entrypoint,copy,add命令的工作目录 用exec进入的默认目录
healthcheck                             //健康检查
```

* 用build构建nginx镜像
    * dockerfile(构建镜像) | nginx-1.12.1.tar.gz(nginx的源码包) | nginx.conf(nginx的配置文件)
    * dockerfile文件内容：
    ```
    #引用镜像
    FROM centos:7

    #说明信息
    MAINTAINER wfc.com

    #安装依赖包
    RUN yum install -y gcc gcc-c++ make openssl-devel pcre-devel
    
    #将nginx-1.12.1.tar.gz放入/tmp
    ADD nginx-1.16.0.tar.gz /tmp

    #进行编译安装操作
    RUN cd /tmp/nginx-1.16.0 && \
        ./configure --prefix=/usr/local/nginx && \
        make -j 2 && \
        make install

    #清理工作
    RUN rm -rf /tmp/nginx-1.16.0* && yum clean all

    #将配置文件拷贝到此路径下
    copy nginx.conf /usr/lcoal/nginx/conf

    #指定工作目录
    workdir /usr/local/nginx

    #声明端口
    EXPOSE 80

    #将容器放入后台操作
    CMD ["./sbin/nginx","-g","daemon off;"]
    ```
    * 开始构建：build命令选项<br>
    docker image build -t [docker镜像仓库名和版本号] \
                    -f [dockerfile的名字] \
                    .    //上下文（.表示当前路径）<br>
    docker image build -t nginx:v1 -f /path/dockerfile /path

* 用build构建PHP镜像
    * Dockerfile | php-5.6.31.tar.gz | php.ini
    * dockerfile文件
    ```
    FROM centos:7
    MAINTAINER www.aliangedu.com
    RUN yum install-y gcc gcc-c++ make gd-devel libxml2-devel libcurl-devel libjpeg-devel libpng-devel openssl-devel
    ADD php-5.6.31.tar.gz /tmp/

    RUN cd /tmp/php-5.6.31 && \
        ./configure --prefix=/usr/local/php \
        --with-config-file-path=/usr/local/php/etc \
        --with-mysql --with-mysqli \
        --with-openssl --with-z]b --with-curl --with-gd \
        --with-jpeg-dir --with-png-dir --with—iconv \
        --enable-fpm --enable-zip --enable-mbstring && \
        make -j 4 && \
        make install && \
        CP /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf && \
        sed -i "s/127.0.0.1/0.0.0.0/" /usr/local/php/etc/php-fpm.conf && \
        sed -i "21a \daemonize = no" /usr/local/php/etc/php-fpm.conf
    COPY php.ini /usr/local/php/etc

    RUN rm -rf /tmp/php-5.6.31* && yum clean all

    WORKDIR /usr/local/php
    ```
    * build打包

构建完镜像的部署工作后要创建自定义网络  docker network create lnmp(通过容器名进行通讯)<br>
容器通过dns解析来解析容器名进行通讯 在nginx容器下ping lnmp_php会去解析php的容器

* 启动PHP容器
```
docker run -itd \
--name lnmp_php \
--net lnmp \
--mount type=bind,src=/app/wwwroot/,dst=/usr/local/nginx/html \
php:v1
```
* 创建nginx容器
```
docker run -itd \
--name lnmp_nginx \
--net lnmp \
-p 888:80 \
--mount type=bind,src=/app/wwwroot/,dst=/usr/local/nginx/html \
nginx:v1
```
* 启动mysql容器<br>
如果之前有部署mysql可能需要删除docker卷 docker volume rm mysql-vol  //删除容器卷
接下来可以尝试重新部署WordPress

__部署tomcat__

dockerfile:
```
from centos:7
maintainer www.aliangedu.com

add jfk-8u45-linux-x64.tar.gz /usr/lcoal    //传入jdk
env java_home /usr/lcal/jdk1.8.0_45 //设置java_home

add apache-tomcat-8.0.46.tar.gz /usr/local  
copy server.xml /usr/lcoal/apache-tomcat-8.0.46/conf

run rm -f /usr/local/*.tar.gz

workdir /usr/lcoal/apache-tomcat-8.0.46
expose 8080
entryponit["./bin/catalina.sh","run"]
```
注意apache默认路径：/app/webapps 缺失会导致容器启动失败

启动容器
```
docker run -itd \
--name=tomcat \
-p 8080:8080 \
--mount type=bind,src=/app/webapps/,dst=/usr/localappache-tomcat-8.0.46/webapps \
tomcat:v1
```