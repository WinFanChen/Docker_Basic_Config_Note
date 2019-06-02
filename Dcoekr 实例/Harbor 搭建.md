## 企业级私有镜像仓库（vmware家的）

__确保已安装 Docker__

__安装 Dockerp-compose__

harbor 由各组件组成，通过 docker-compose 来启动
* 下载 dockerp-compose 文件并赋予执行权限，[官方文档](https://docs.docker.com/compose/install/)详细说明了这两个步骤

__安装 Harbor__
* 下载[离线安装包](https://github.com/goharbor/harbor/releases)
* 解压 tar 包并进入
```
tar zxvf harbor-offline-installer-vx.x.0.tgz
```
* 创建一个 cert 文件夹进行证书操作
* 在 cert 下[生成服务器的 https 公钥私钥](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/Dcoekr%20实例/使用%20openssl%20实现%20https%20证书.md)

__编辑配置文件 Harbor.yml__
```
hostname: 172.28.187.21

https:
  # https port for harbor, default is 443
  port: 443
  # The path of cert and key files for nginx
  certificate: /data/harbor/cert/172.28.187.21.crt
  private_key: /data/harbor/cert/172.28.187.21.key

harbor_admin_password: Harbor12345
```
__运行 harbor__

* 变更配置
```
./prepare
```
* 运行
```
./install.sh
```
* 查看当前 harbor 各组件运行状态
```
docker-compose ps
```

__浏览器访问 https://172.28.187.21__

* 创建一个 test 项目
* 创建 chen 用户
* 登陆用户后
```
    mkdir /etc/docker/certs.d/172.28.187.21 -p
```

__登陆成功后__
```
    docker tag tomcat:v1 reg.aliangedu.com/test/tomcat:v1
    docker push reg.aliangedu.com/test/tomcat:v1
```