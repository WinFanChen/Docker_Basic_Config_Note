## 官方有一个 Registry 的 doker 镜像可以让宿主机实现存储私有镜像

之前可以通过docker iamge save将镜像进行导出 我们玩个高级一点的：搭建私有仓库

docker hub 是官方的公共镜像 官方提供了registry 镜像来搭建私有仓库
* 下载 registry
```
docker pull registry
```
运行 registry 将镜像持久化在 var/lib/registry 下并暴露 5000 端口，此宿主机就作为了 docker 镜像的提供仓库
```
docker run -d -v /opt/registry:/var/lib/registry -p 5000:5000 --restart=always --name registry registry
```
* 我们可以用 curl 来获取所有的存储的镜像列表
```
curl 172.28.187.21:5000/v2/_catalog
```

* 配置推送端的私有仓库：还记得怎么配置仓库地址吗？
```
/etc/docker/daemon.json

{
    "insecure-registries":["docker仓库IP地址:5000"]
}
```
* 重启 docker 后才能生效
* 对要提交的镜像打标签（标注产地）
```
docker tag nginx:1.12 172.28.187.21:5000/nginx:1.12
```
* 提交镜像
```
docker push 仓库宿主机ip地址:5000/nginx:1.12
```
* 拉取镜像
```
docker pull 仓库宿主机ip地址:5000/nginx:1.12
```

