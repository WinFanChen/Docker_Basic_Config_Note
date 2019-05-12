解决镜像存放的位置 官方Registry的镜像仓库

通过docker iamge save进行导出

搭建私有仓库

docker hub是官方的公共镜像 官方提供了registry镜像来搭建私有仓库

docker pull registry //下载registry
docker run -d -v /opt/registry:/var/lib/registry -p 5000:5000 --restart=always --name registry registry //将镜像持久化在var/lib/registry下并暴露5000端口，此宿主机就作为了docker镜像的提供仓库

我们可以用 curl 仓库宿主机ip地址:5000/v2/_catalog 来获取所有的存储的镜像列表

配置私有仓库：还记得怎么配置仓库地址吗？
/etc/docker/daemon.json
{
    "insecure-registries":["192.168.0.212:5000"]
}
还需要重启docker生效

docker tag nginx:1.12 仓库宿主机ip地址:5000/nginx:1.12  //对要提交的镜像打标签（标注产地）

docker push 仓库宿主机ip地址:5000/nginx:1.12    //提交镜像

奇淫技巧：docker rmi -f $(docker images -q -a)

docker pull 仓库宿主机ip地址:5000/nginx:1.12