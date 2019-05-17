# Docker_Basic_Config_Note

2019/4/30   Bilibili-[一天掌握Docker](https://www.bilibili.com/video/av49731612)<br>
本来想在WLS上实现docker的功能 但是没有成功 转战在虚拟机上使用 CentSO部署成功<br>

2019/5/7 昨晚上微软公布了新的WLS2的计划可以原生运行Docker -真厉害！看来虚拟机可以被取代了？<br>

2019/5/9 昨天晚上跟好友（介绍我的朋友[毛寅滔](https://github.com/yiluomyt) 很厉害呦~ [博客地址](https://blog.mytyiluo.cn/)）聊DevOps的东西 觉得蛮有意思的 记录一下:<br>
>DevOps的范围最大，敏捷算是一种软件开发模式，持续集成是在敏捷开发的要求下延伸的<br>
引入azure pipelines解决docker的配置变更->pipelines和git库绑定以触发自动化流程->可以用部署流程触发自动化部署把docker镜像推送到服务器->docker容器过多需要管理的话有compose或者k8s->再往后可能就做些运行健康状态监控之类的

2019/5/13 华为的DevOpsCloud搞了一个活动让开发者来接触这套DevOps的平台，确实让我大开眼界。从编码到测试到发布 真正的做到了持续集成和自动化部署，真厉害！
>敏捷和devops的关系：敏捷是开发的思路 devops是实现的方式<br>
    提升效能，市场变化来改进自身速度减小管理单元，减小工程之间的耦合

+ [将Docker部署在CentOS上](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/B站-一天掌握Docker/部署在CentOS上.md)<br>
+ [管理镜像](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/B站-一天掌握Docker/怎么管理镜像.md)<br>
+ [管理容器](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/B站-一天掌握Docker/怎么管理容器.md)<br>
+ [管理应用程序数据](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/B站-一天掌握Docker/管理应用程序数据.md)<br>
+ [搭建一个LNMP的项目——WordPress](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/B站-一天掌握Docker/用LNMP平台搭建WordPress.md)<br>
+ [怎么打包自己的容器镜像？ build与dockerfile](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/B站-一天掌握Docker/Dockerfile的领域.md)<br>
+ [用Registry来搭建自己的docker镜像仓库](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/B站-一天掌握Docker/用Registry来搭建自己的私有docker仓库.md)<br>
+ [Docker Hub](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/B站-一天掌握Docker/Docker%20Hub.md)
+ [如果需要企业级私有仓库：Harbor](https://github.com/lcePolarBear/Docker_Basic_Config_Note/blob/master/B站-一天掌握Docker/选修：Harbor企业级私有镜像搭建.md)