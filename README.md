# docker
learn docker
- [docker 概述](#Docker概述)
- [docker 安装](#docker安装)
- [docker 命令](#docker命令)
- [docker 镜像](#docker镜像)
- [容器数据卷](#docker命令)
- [dockerFile](#docker命令)
- [docker网络原理](#docker命令)
- [IDEA整合docker](#docker命令)
- [docker compose](#docker命令)
- [docker swarm（简化版k8s）](#docker命令)
- [CI\CD JENKINS](#docker命令)

Docker概述 

Docker为什么出现？
1. 开发-上线俩套环境！ 应用环境，配置
2. 开发人员，运维人员
3. 版本更新导致服务不可用
4. 环境配置十分的麻烦，每一个机器都要部署环境（集群redis，es）！费时费力
5. 项目带上环境进行安装打包。
6. 环境不能跨平台
7. 开发使用Windows 最后发布到Linux 

Docker 思想
docker 中心思想源于它的logo
1. 隔离：集装箱 例如之前多个项目之间会有冲突，eg 端口冲突，版本冲突等等。

 
```bash
#查看所有的docker 镜像
$docker ps -a

#查看正在运行的docker容器
$docker ps

#重启正在运行的docker容器
$docker restart <imageId>

#启动docker容器
$docker start <imageId>

#停止docker容器
$docker stop <imageId>

#删除docker容器
$docker rm <imageId>

#修改容器名
docker rename <my_container_name> <my_new_container_name>

#进入docker容器
$docker exec -it nginx  /bin/bash

#挂载目录并运行
docker run -d --name <iamgeName> -p 3030:80 -v E:/projectE/new_uplink_use_git/new_uplink_payment:/opt/usen/uplink/current wqcyber/new_uplink_php:v2
```
  
   
  
  
  
 

## docker 镜像上传到 Docker Hub 仓库

### 1.将docker 容器提交为docker镜像
```bash
docker commit -a "duanzhigang" -m "nginx test" 352ea94c14be dzg_nginx:v1
```

参数说明；

-a :提交的镜像作者；

-c :使用Dockerfile指令来创建镜像；

-m :提交时的说明文字；

-p :在commit时，将容器暂停

### 2.将docker 镜像上传到Docker Hub
```bash
docker push duanzhigang/dzg_nginx:v1
```
