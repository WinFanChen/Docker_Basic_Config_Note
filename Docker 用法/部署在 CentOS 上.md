[官方部署说明](https://docs.docker.com/install/linux/docker-ce/centos/)

只要完全按着说明部署就可以完成

docker 安装步骤
```bash
yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2

yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

yum install -y docker-ce docker-ce-cli containerd.io

systemctl start docker

systemctl enable docker
```
[脚本链接](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/%E6%89%80%E9%9C%80%E8%A6%81%E7%9A%84%E6%96%87%E4%BB%B6/docker_install_secipt.sh)

首先保证本地时间与docker服务器的时间保持一致！不然镜像都拉不下来

[docker国际镜像](https://hub.docker.com/search?&q=)中有大量常用镜像

更新 Docker 使用国内的的镜像仓库
```json
# /etc/docker/daemon.json

{
    "registry-mirrors":["https://registry.docker-cn.com","http://hub-mirror.c.163.com","https://docker.mirrors.ustc.edu.cn"]
}
```

[中国区加速拉取镜像](https://www.cnblogs.com/weifeng1463/p/7468391.html)
