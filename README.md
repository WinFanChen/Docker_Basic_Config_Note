# Docker 基础配置备忘录

## 用法
+ [部署在 CentOS](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/Docker%20用法/部署在%20CentOS上.md)
+ [管理镜像](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/Docker%20用法/怎么管理镜像.md)
+ [管理容器](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/Docker%20%E7%94%A8%E6%B3%95/%E6%80%8E%E4%B9%88%E7%AE%A1%E7%90%86%E5%AE%B9%E5%99%A8.md)
+ [管理应用程序数据](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/Docker%20用法/管理应用程序数据.md)
+ [Build+Dockerfile](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/Docker%20用法/Dockerfile%20的领域.md)
+ [Registry 搭建私有仓库](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/Docker%20用法/用%20Registry%20来搭建自己的私有%20docker%20仓库.md)
+ [Docker Hub 公有仓库](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/Docker%20用法/Docker%20Hub.md)

## 实例
+ [搭建博客 WordPress](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/Dcoekr%20实例/用%20LNMP%20平台搭建%20WordPress.md)
+ [搭建企业级私有仓库 Harbor](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/Dcoekr%20实例/Harbor%20搭建.md)

## 碎碎念
__2019/4/30 B站-[一天掌握Docker](https://www.bilibili.com/video/av49731612)__<br>
* 现在在WLS上无法实现docker的功能，但微软公布了新的WLS2的计划可以原生运行Docker -真厉害！看来虚拟机可以被取代了？<br>
* 2019/5/9    昨天晚上[毛寅滔](https://blog.mytyiluo.cn/)([GitHub](https://github.com/yiluomyt))把他理解的 DevOps 跟我说了一下，觉得说的很好，拿来引用：
    > DevOps 的范围最大，敏捷算是一种软件开发模式，持续集成是在敏捷开发的要求下延伸的

    > 引入 azure pipelines 解决 docker 的配置变更-> pipelines 和 git 库绑定以触发自动化流程-> 可以用部署流程触发自动化部署把 docker 镜像推送到服务器-> docker 容器过多需要管理的话有 compose 或者 k8s-> 再往后可能就做些运行健康状态监控之类的（[联动我的运维工具库](https://github.com/lcePolarBear/Ops_Automation_Note)）

* 2019/5/13   华为的DevOpsCloud搞了一个活动让开发者来接触这套DevOps的平台，确实让我大开眼界。从编码到测试到发布 真正的做到了持续集成和自动化部署，真厉害！
    > 敏捷和devops的关系：敏捷是开发的思路 DevOps 是实现的方式

__2019/6/03 Bilibili-[Jenkins 与 Docker/Kubernetes 的自动化 CI/CD 实践](https://www.bilibili.com/video/av49787649)__
* 之前跟[毛寅滔](https://blog.mytyiluo.cn/)聊 DevOps 提到通过 azure pipelines 触发自动化流程，那么 Jenkins 就是 azure pipelines 的同类产品，通过示范体会到了自动化流程的魅力
    > CI 代码构建测试部署轮回重复<br>
      CD 各种环境部署和生产环境的发布