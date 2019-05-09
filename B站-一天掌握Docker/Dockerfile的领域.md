Dockerfile指令

看样子是用来构建自己的镜像

from centos:7
maintainer www.aliangedu.com
run yum install -y gcc gcc-c++ make gd-devel libxm12- //构建镜像时运行shell命令
cmd ["./sbin/php-ftp","-c","/usr/local/php/etc/php-ftp.conf] //运行镜像时运行shell命令 用数组实现 一般用来启脚本什么的
expose //声明端口
env java_home /usr/lcoal/jdk1.8.0_45 //声明容器内环境变量java_home
add php-5.6.31.tar.gz /tmp/ //拷贝文件/目录到镜像 不建议使用url 压缩包会自动解压
copy 无解压功能的add
entrypoint 在使用docker run [options] image [command] 时接收command
volume //还记得在run时的挂载吗? 这个不常用
user root //使用 root 用户权限执行run,cmd,entrypoint命令
workdir /data//设定run,cmd,entrypoint,copy,add命令的工作目录 用exec进入的默认目录
healthcheck //健康检查

build镜像

dockerfile+配置文件

构建nginx所需要到的 -> dockerfile(构建镜像) nginx-1.12.1.tar.gz(nginx的源码包)   nginx.conf(nginx的配置文件)
dockerfile：
form centos:7   //引用镜像
maintainer www.aliangedu.com    //说明信息
run yum install -y gcc gcc-c++ make openssl-devel pcre-devel    //安装依赖包
add nginx-1.12.1.tar.gz /tmp    //将nginx-1.12.1.tar.gz放入/tmp

run cd /tmp/nginx-1.12.1 && \
    ./configure --prefix=/usr/lcoal/nginx && \
    make -j 2 && \
    make install    //进行编译安装操作

run rm -rf /tmp/nginx-1.12.1* && yum clean all  //清理工作

copy nginx.conf /usr/lcoal/nginx/conf   //将配置文件

workdir /usr/local/nginx    //指定工作目录
expose 80
cmd ["./sbin/nginx", "-g", "daemon off;"]

开始构建了：build命令选项
docker image build -t [docker镜像仓库名和版本号] \
                   -f [dockerfile的名字] \
                   .    //上下文（.表示当前路径）
docker image build -t nginx:v1 -f /path/dockerfile /path

构建PHP所需要到的   Dockerfile  php-5.6.31.tar.gz   php.ini
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

构建完镜像的部署工作
创建自定义网络  docker network create lnmp(通过容器名进行通讯)
容器通过dns解析来解析容器名进行通讯 在nginx容器下ping lnmp_php会去解析php的容器

创建PHP容器
docker run -itd \
--name lnmp_php \
--net lnmp \
--mount type=bind,src=/app/wwwroot/,dst=/usr/local/nginx/html \
php:v1

创建nginx容器
docker run -itd \
--name lnmp_nginx \
--net lnmp \
-p 888:80 \
--mount type=bind,src=/app/wwwroot/,dst=/usr/local/nginx/html \
nginx:v1

启动mysql容器
如果之前有部署mysql可能需要删除docker卷 docker volume rm mysql-vol  //删除容器卷
接下来可以尝试重新部署WordPress