## 官方有一个Registry的doker镜像可以让宿主机实现存储私有镜像

之前可以通过docker iamge save将镜像进行导出 我们玩个高级一点的

* 搭建私有仓库

docker hub 是官方的公共镜像 官方提供了registry 镜像来搭建私有仓库

> docker pull registry //下载registry<br>
> docker run -d -v /opt/registry:/var/lib/registry -p 5000:5000 --restart=always --name registry registry //将镜像持久化在var/lib/registry下并暴露5000端口，此宿主机就作为了docker镜像的提供仓库

我们可以用 curl 仓库宿主机ip地址:5000/v2/_catalog 来获取所有的存储的镜像列表

* 配置推送端的私有仓库：还记得怎么配置仓库地址吗？
```
/etc/docker/daemon.json
{
    "insecure-registries":["docker仓库IP地址:5000"]
}
```
重启docker后才能生效

>docker tag nginx:1.12 仓库宿主机ip地址:5000/nginx:1.12  //对要提交的镜像打标签（标注产地）<br>
docker push 仓库宿主机ip地址:5000/nginx:1.12    //提交镜像<br>
docker pull 仓库宿主机ip地址:5000/nginx:1.12    //拉取镜像

奇淫技巧：docker rmi -f $(docker images -q -a)（用来删除docker下所有的镜像）

