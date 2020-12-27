docker 学习笔记

# 只要学不死，就往死里学！！
- [只要学不死，就往死里学！！](#只要学不死就往死里学)
  - [Docker概述](#docker概述)
    - [Docker为什么出现？](#docker为什么出现)
    - [Docker 思想](#docker-思想)
    - [Docker 历史](#docker-历史)
    - [聊聊Docker](#聊聊docker)
    - [Docker 能干什么](#docker-能干什么)
      - [之前的虚拟机技术](#之前的虚拟机技术)
      - [容器化技术](#容器化技术)
    - [docker与传统虚拟机的不同](#docker与传统虚拟机的不同)
    - [DevOps（开发，运维）](#devops开发运维)
      - [应用更快速的交付和部署](#应用更快速的交付和部署)
      - [更便捷的升级和扩缩容](#更便捷的升级和扩缩容)
      - [更简单的系统运维](#更简单的系统运维)
      - [更高效的计算资源利用](#更高效的计算资源利用)
  - [docker安装](#docker安装)
    - [Docker的基本组成](#docker的基本组成)
    - [环境准备](#环境准备)
  - [docker命令](#docker命令)
  - [docker镜像](#docker镜像)
  - [容器数据卷](#容器数据卷)
  - [dockerFile](#dockerfile)
  - [docker网络原理](#docker网络原理)
  - [IDEA整合docker](#idea整合docker)
  - [docker Compose](#docker-compose)
  - [dockerSwarm（简化版k8s）](#dockerswarm简化版k8s)

## Docker概述 
### Docker为什么出现？
1. 开发-上线俩套环境！ 应用环境，配置
2. 开发人员，运维人员
3. 版本更新导致服务不可用
4. 环境配置十分的麻烦，每一个机器都要部署环境（集群redis，es）！费时费力
5. 项目带上环境进行安装打包。
6. 环境不能跨平台
7. 开发使用Windows 最后发布到Linux 
### Docker 思想
docker 中心思想源于它的logo
1. 隔离：集装箱 例如之前多个项目之间会有冲突，eg 端口冲突，版本冲突等等。
2. docker 可以将服务器利用到极致
3. 最后docker解决了这些问题 将环境和代码同时打包成镜像
### Docker 历史
2010年IT年轻人在美国成立了一家公司叫 dotCloud 做一些pass的云计算服务 Linux 的容器技术。 

2013年开源 火了 
2014年4月9日 Docker1.0 发布
Docker为
### 聊聊Docker
docker 是基于go语言开发 

官网：https://www.docker.com 

docker 文档非常详细  

仓库地址 https://www.docker.hub.com
### Docker 能干什么
#### 之前的虚拟机技术
   缺点
   1. 资源占用多
   2. 冗余步骤多
   3. 启动慢
#### 容器化技术
- 容器化技术不是完整的模拟一个完整的操作系统
### docker与传统虚拟机的不同
1. 传统的虚拟机，虚拟出一套完整的硬件，运行一个完整的操作系统，然后在这个系统上安装和运行软件
2. 容器内应用直接运行在宿主机额内容，容器是没有自己的内核的，也没有虚拟我们的硬件，所有就轻便了
3. 每个容器间是互相隔离的，每个容器都一个属于自己的文件系统，互不影响

### DevOps（开发，运维）
#### 应用更快速的交付和部署
传统：一堆帮助文档，安装程序
Docker：一键运行
#### 更便捷的升级和扩缩容
使用了Docker之后，部署应用就和搭积木一样
项目打包成一个镜像，一键扩展
#### 更简单的系统运维
在容器化之后，开发和测试环境都是高度一致 
#### 更高效的计算资源利用
Docker 是内核级别的虚拟化，可以在物理机上可以运行多个运行实例

## docker安装 
### Docker的基本组成  
1. 镜像（image）
   docekr镜像就好比一个模板，可以通过这个模板来创建容器服务。
2. 容器（container）
    docker利用容器技术，独立运行一个或者一组应用，通过镜像来创建
3. 仓库（repository）
   仓库就是存放镜像的地方
   仓库分为共有仓库和私有仓库
   官方的Docker Hub
   阿里云
   配置镜像加速
### 环境准备
## docker命令 
## docker镜像 
## 容器数据卷 
## dockerFile
## docker网络原理 
## IDEA整合docker 
## docker Compose 
## dockerSwarm（简化版k8s） 
 
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
  
   
  
  
  
 

 docker 镜像上传到 Docker Hub 仓库

 1.将docker 容器提交为docker镜像
```bash
docker commit -a "duanzhigang" -m "nginx test" 352ea94c14be dzg_nginx:v1
```

参数说明；

-a :提交的镜像作者；

-c :使用Dockerfile指令来创建镜像；

-m :提交时的说明文字；

-p :在commit时，将容器暂停

 2.将docker 镜像上传到Docker Hub
```bash
docker push duanzhigang/dzg_nginx:v1
```
