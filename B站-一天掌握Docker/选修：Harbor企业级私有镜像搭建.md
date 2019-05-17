## 企业级私有镜像仓库（vmware家的）

__本机安装好Docker|Dockerp-compose__<br>
    下载：sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    解压：unzip docker-compose-linux-x86_64.zip
    授权：sudo chmod +x /usr/local/bin/docker-compose

__[自签TLS证书](https://github.com/goharbor/harbor/blob/master/docs/configure_https.md)__<br>
    解压tar包并进入：tar zxvf harbor-offline-installer-v1.4.0.tgz<br>
    创建一个ssl的文件夹进行证书操作<br>
    比着官方说明进行操作<br>

__[下载安装包](https://storage.googleapis.com/harbor-releases/release-1.7.0/harbor-offline-installer-v1.7.5.tgz)__

__配置__
```
    harbor.cfg<br>
    hsotname<br>
    ui<br>
    ssl_cert<br>
    ssl_cert_key<br>

    harbor_admin_passwd
```
__运行 prepare__

__运行 install.sh__

__docker compose ps 会通过一个yml文件来看当前容器__<br>
    在C:/windwos/system32/drivers/etc/host文件添加:192.168.0.213 reg.aliangedu.com

__浏览器访问 reg.aliangedu.com__


__创建一个test项目__<br>
创建aliang用户


在docker机器下<br>
你用 docker login reg.aliangedu.com 是访问不到的<br>
也要先添加host<br>
vi /etc/hosts 添加  192.168.0.213 reg.aliangedu.com<br>

__登陆用户后__<br>
```
    mkdir /etc/docker/certs.d/reg.aliangedu.com -p
    scp root@192.168.0.213:/root/harbor/ssl/reg.aliangedu.com.crt /etc/docker/certs.d/reg.aliangedu.com
    scp root@192.168.0.213:/root/harbor/ssl/reg.aliangedu.com.key /etc/docker/certs.d/reg.aliangedu.com
```
__登陆成功后__
```
    docker tag tomcat:v1 reg.aliangedu.com/test/tomcat:v1
    docker push reg.aliangedu.com/test/tomcat:v1
```