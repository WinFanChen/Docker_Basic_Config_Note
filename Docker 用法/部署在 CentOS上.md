[官方部署说明](https://docs.docker.com/install/linux/docker-ce/centos/)

只要完全按着说明部署就可以完成

[docker 安装脚本](docker_install_secipt.sh)
```
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

首先保证本地时间与docker服务器的时间保持一致！不然镜像都拉不下来

[docker国际镜像](https://hub.docker.com/search?&q=)中有大量常用镜像

更新 Docker 使用国内的的镜像仓库
- 编辑路径：/etc/docker/daemon.json
    ```
    {
        "registry-mirrors":["https://registry.docker-cn.com"]
    }
    ```

[中国区加速拉取镜像](https://www.cnblogs.com/weifeng1463/p/7468391.html)
