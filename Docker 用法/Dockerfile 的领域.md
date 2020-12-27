## Dockerfile指令
docker image build 命令通过 dockerfile 文件来构建镜像

__dockerfile文件示例__
```
from centos:7                           //表示从什么地方继承镜像内容
maintainer zhao chen                    //填写维护信息
run yum install...                      //构建镜像时运行shell命令
add php-5.6.31.tar.gz /tmp/             //拷贝文件/目录到镜像 不建议使用url 压缩包会自动解压
copy                                    //无解压功能的add
entrypoint                              //在使用docker run [options] image [command] 时接收command
user root                               //使用 root 用户权限执行run,cmd,entrypoint命令
env java_home /usr/lcoal/jdk1.8.0_45    //声明容器内环境变量java_home
volume                                  //还记得在run时的挂载吗? 这个不常用
workdir /data                           //设定run,cmd,entrypoint,copy,add命令的工作目录 用exec进入的默认目录
expose 80                               //声明端口
healthcheck                             //健康检查
cmd ["./sbin/php-ftp","-c",...]         //运行镜像时运行shell命令 用数组实现 一般用来启脚本什么的
```

### __用build构建nginx镜像__
* 所需文件：
    * [dockerfile](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/Docker%20用法/Dockerfile)(构建镜像)
    * [nginx-1.12.1.tar.gz](http://nginx.org/download/nginx-1.15.5.tar.gz)(nginx的源码包)
    * nginx.conf(nginx的配置文件)
   
* 开始构建：docker image build +
    * -t [docker镜像仓库名和版本号]
    * -f [dockerfile的名字]
    * .（表示当前路径）
    ```
    docker image build -t nginx:v1 -f Dockerfile .
    ```
* 运行生成的 nginx 镜像
    ```
    docker run -d --name nginx01 -p 88:80 nginx:v1
    ```
    
__创建docker网络__

* 构建完镜像的部署工作后要创建自定义网络  docker network create lnmp(通过容器名进行通讯)<br>
* 容器通过dns解析来解析容器名进行通讯 在nginx容器下ping lnmp_php会去解析php的容器