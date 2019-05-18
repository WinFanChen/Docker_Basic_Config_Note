#引用镜像
FROM centos

#说明信息
LABEL maintainer="wfc@outlook.com"

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
COPY nginx.conf /usr/lcoal/nginx/conf

#指定工作目录
WORKDIR /usr/local/nginx

#声明端口
EXPOSE 80

#将容器放入后台操作
CMD ["./sbin/nginx","-g","daemon off;"]