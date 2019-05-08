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