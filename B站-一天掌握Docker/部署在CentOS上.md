## [官方部署说明](https://docs.docker.com/install/linux/docker-ce/centos/)
只要完全按着说明部署就可以完成

[docker国际镜像](https://hub.docker.com/search?&q=)中有大量常用镜像

更新Docker使用国内的的镜像仓库<br>
编辑路径：/etc/docker/daemon.json

    {
        "registry-mirrors":["https://registry.docker-cn.com"]
    }

docker images   查看本地安装的docker镜像

docker pull nginx	拉取nginx<br>
docker pull nginx:1.12	特定版本

[中国区加速拉取镜像](https://www.cnblogs.com/weifeng1463/p/7468391.html)

容器就是在镜像上铺的一层读写层

容器性能的好坏取决于存储驱动	Ubuntu-aufs |	CentOS-devicemaapper
