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
    - [帮助文档](#帮助文档)
    - [阿里云镜像加速](#阿里云镜像加速)
  - [docker命令](#docker命令)
    - [docker是怎么工作的](#docker是怎么工作的)
    - [docker为什么比VM快](#docker为什么比vm快)
    - [常用命令](#常用命令)
      - [1.帮助命令](#1帮助命令)
      - [2.镜像命令](#2镜像命令)
      - [3.容器命令](#3容器命令)
      - [4.退出容器](#4退出容器)
      - [5.删除容器](#5删除容器)
      - [6.启动和停止容器](#6启动和停止容器)
    - [常用命令其他命令](#常用命令其他命令)
      - [后台启动容器](#后台启动容器)
      - [查看日志](#查看日志)
      - [查看容器中的进程信息](#查看容器中的进程信息)
      - [查看容器中元数据](#查看容器中元数据)
      - [进入当前正在运行的容器](#进入当前正在运行的容器)
      - [从容器内拷贝文件到主机上](#从容器内拷贝文件到主机上)
  - [docker镜像](#docker镜像)
    - [镜像是什么](#镜像是什么)
    - [Docker镜像加载原理](#docker镜像加载原理)
    - [UnionFS（联合文件系统）](#unionfs联合文件系统)
    - [分层理解](#分层理解)
    - [commit镜像](#commit镜像)
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
### 帮助文档
```shell
# 1.卸载旧版本
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine 

# 2.需要的安装包
$ sudo yum install -y yum-utils

# 3.设置镜像仓库
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo #默认的是国外的
    修改为阿里云的国内镜像仓库或者配置yum源

# 4.安装docker相关的内容
# 更新yum软件包索引
# docker-ce 社区版 ee 企业版
$ sudo yum install docker-ce docker-ce-cli containerd.io

# 5.启动docker
$ sudo systemctl start docker

# 6.测试docker
$ docker version
$ sudo docker run hello-world

# 7. 查看下载的hello-world镜像
$ sudo docker images
PS C:\WINDOWS\system32> docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    bf756fb1ae65   11 months ago   13.3kB

# 8. 卸载docker
$ sudo yum remove docker-ce docker-ce-cli containerd.io
$ sudo rm -rf /var/lib/docker
```
### 阿里云镜像加速
1. 登录阿里云
2. 找到镜像加速的位置
3. 有镜像加速器
4. 执行命令
   ```shell
   sudo mkider -p /etc/docker

   sudo tee /etc/docker/daemon.json<<-'EOF'
   {
       "registry-mirrors":["https://qiyb99977.mirror.aliyuncs.com"]
   }
   EOF
   sudo systemctl daemon-reload
   sudo systemctl restart docker
   ```
## docker命令 
### docker是怎么工作的
docker是一个CS 架构的系统。通过Socket从客户端访问。
DockerServer接收到Docker-Clint的指令，就会执行这个命令。
### docker为什么比VM快
1. docker有着比虚拟机更少的抽象层
2. docker利用的是宿主的内核，VM需要的是GuestOS
新建一个容器的时候，docker不需要像虚拟机一样重新加载一个操作系统内核，避免引导，虚拟机是加载GuestOS，分钟级别的。虚拟机是硬件虚拟化。而docker是利用宿主主机的操作系统，省略了这个复杂的过程。
### 常用命令
#### 1.帮助命令
```bash
   docker version #显示docker的版本信息
   docker info #详细信息 系统信息
   docker 命令 --help #万能命令
```
#### 2.镜像命令
```bash
docker images #查看镜像信息

PS C:\WINDOWS\system32> docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    bf756fb1ae65   11 months ago   13.3kB
# 解释
REPOSITORY 镜像的仓库源
TAG 镜像的标签
IMAGE ID 镜像的ID
CREATED 创建时间
SIZE 大小
Options:
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs 

  
  docker search mysql #搜索镜像
  Options:
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results (default 25)
      --no-trunc        Don't truncate output
PS C:\WINDOWS\system32> docker search mysql --filter=STARS=3000
NAME      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql     MySQL is a widely used, open-source relation…   10312     [OK]
mariadb   MariaDB is a community-developed fork of MyS…   3822      [OK]

#精髓
docker pull #下载镜像

PS C:\WINDOWS\system32> docker pull mysql
Using default tag: latest #如果不写tag，默认就是lastes
latest: Pulling from library/mysql
6ec7b7d162b2: Pull complete #分层下载，docker image 的核心 联合文件系统
6ec7b7d162b2: Pull complete
6ec7b7d162b2: Pull complete
6ec7b7d162b2: Pull complete
Digest: sha256:78800e6d3f1b230e35275145e657b82c3fb02a27b2d8e76aac2f5e90c1c30873 #签名
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest #真实地址


docker rmi # 删除镜像 可通过name 和 image id
docker rmi -f $(docker images -aq) #递归删除全部镜像
```
#### 3.容器命令
```bash
# 新建容器并启动
docker run [可选参数] image
# 参数说明
--name="NAME" # 容器名字 同来区分容器
-d # 后台方式运行
-it # 使用交互的方式运行，进入容器查看内容
-p # 指定容器的端口 -p 8080:8080
  1. -p ip:主机端口:容器端口
  2. -p 主机端口：容器端口
  3. -p 容器端口
  4. 容器端口
-p # 随机指定端口

docker run -it [容器NAME] /bin/bash # 启动并进入容器

exit # 从容器中退出到主机

docker ps # 查看当前正在运行的容器
docker ps -a # 列出当前正在运行的容器，带出历史运行过的容器
docker ps -n
```
#### 4.退出容器
```bash
exit # 直接退出容器并退出
Ctrl + Q + P #容器不停止并退出
```
#### 5.删除容器
```bash
docker rm 容器id # 删除所有容器 不能删除正在运行的容器 如果强制删除的使用 rm -f
docker rm -f $(docekr ps -aq) # 删除所有容器
docker ps -a -q|xargs docker rm # 删除所有容器
```
#### 6.启动和停止容器
```bash
docker start 容器id # 启动容器 
docker restart # 重启容器
docker stop # 停止容器
docker kill # 强制停止容器
```
### 常用命令其他命令
#### 后台启动容器
```bash
docker run -d 镜像名 # 启动容器 
```
#### 查看日志
```bash
docker logs 容器id# 查看日志 
docker run --name="test-nginx"  -d nginx /bin/sh -c "while true;do echo duan;sleep 1;done" # 自己编写shell脚本 测试日志
docker logs -tf --tail 10 a07511fd425b # 显示指定行日志
```
#### 查看容器中的进程信息
```bash
docker top 镜像id 
```
#### 查看容器中元数据
```bash
docker inspect 镜像id
```
#### 进入当前正在运行的容器
```bash
# 我们容器通常都是使用后台方式运行的，需要进入容器，修改一些配置
# 命令1
docker exec -it a07511fd425b /bash
# 命令2
docker attach 容器id
```
#### 从容器内拷贝文件到主机上
```bash
docker cp 0754eec7b305:/home/test.java ./  
```
## docker镜像 
### 镜像是什么
镜像是一个轻量级的可执行的独立软件包，用来打包软件运行环境和基于运行环境开发的软件，它包含运行某个软件所需的所有内容，包括代码，运行时，库，环境变量和配置文件。
所有的应用，直接打包docker镜像，就可以直接跑起来。
如何得到镜像
1. 从远程仓库下载
2. 朋友copy给你
3. 自己制作一个镜像DockerFile
### Docker镜像加载原理
### UnionFS（联合文件系统）
### 分层理解 
分层下载 重复复用
### commit镜像
```bash
docker commit # 提交容器成为一个新的副本
docker commit -m="描述信息" -a="作者" 容器id 目标镜像名 tag
# docker 镜像上传到 Docker Hub 仓库
docker commit -a "duanzhigang" -m "nginx test" 352ea94c14be dzg_nginx:v1

参数说明:
-a :提交的镜像作者；

-c :使用Dockerfile指令来创建镜像；

-m :提交时的说明文字；

-p :在commit时，将容器暂停

 2.将docker 镜像上传到Docker Hub
docker push duanzhigang/dzg_nginx:v1
```
## 容器数据卷
### 匿名挂载&具名挂载
```bash
# 匿名挂载
-v 容器内地址
-P 随机指定端口
docker run -d -P --name nginx01 -v /etc/nginx nginx

# 查看所有的 volume 的情况
docker volume ls
# -v 没有指定容器外路径只指定了内部容器地址

# 具名挂载
#查看卷位置 没有指定目录的情况下  没有指定目录的情况下都在 /var/lib/docker/volumes/xxxx/_data
#通过具名挂载可以方便找到卷的位置
PS C:\Windows\system32> docker volume inspect juming-nginx
[
    {
        "CreatedAt": "2021-01-04T02:05:53Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/juming-nginx/_data",
        "Name": "juming-nginx",
        "Options": null,
        "Scope": "local"
    }
]
```
### 如何区分具名挂载、匿名挂载、指定容器挂载
```bash
-v 容器内路径 # 匿名挂载
-v 卷名：容器内路径 # 具名挂载
-v /宿主机路径：容器内路径 # 指定路径挂载

# 拓展
docker run -d -P --name nginx01 -v juming-nginx:/etc/nginx:ro nginx
docker run -d -P --name nginx01 -v juming-nginx:/etc/nginx:rw nginx

ro read only #只读 只能通过宿主机操作，不同通过容器内修改
rw read write #可读可写
# 一旦设置了容器权限，容器对我们挂载的内容就有限定。
```
### dockerFile方式实现挂载文件
DockerFile 就是用来构建Docker镜像的构建文件。命令脚本,通过这个脚本生成一个脚本。
镜像是一层一层的，脚本是一个个的命令，每个命令都是一层。

```bash
# 创建一个dockerFile，名字可以随机，建议使用Dockerfile
# 文件中的内容 指令（大写） 参数
FROM centos

VOLUME ["volume01","volume02"]

CMD echo "------end----"

CMD /bin/bash

# 这里每个命令都是镜像的一层

# 执行dockerFile文件
docker build -f dockerfile1 -t dzg/centos:1.0 .

root@DESKTOP-55LGOP2:/home/docker-test-volume# docker build -f dockerfile1 -t dzg/centos:1.0 .
Sending build context to Docker daemon  2.048kB
Step 1/4 : FROM centos
latest: Pulling from library/centos
7a0437f04f83: Pull complete
Digest: sha256:5528e8b1b1719d34604c87e11dcd1c0a20bedf46e83b5632cdeac91b8c04efc1
Status: Downloaded newer image for centos:latest
 ---> 300e315adb2f
Step 2/4 : VOLUME ["volume01","volume02"]
 ---> Running in 0cc6fac12531
Removing intermediate container 0cc6fac12531
 ---> bfe48ab0dcc0
Step 3/4 : CMD echo "------end----"
 ---> Running in ef9e250886db
Removing intermediate container ef9e250886db
 ---> 6b45bba8d564
Step 4/4 : CMD /bin/bash
 ---> Running in ae165fe7fc76
Removing intermediate container ae165fe7fc76
 ---> bd1940211df9
Successfully built bd1940211df9
Successfully tagged dzg/centos:1.0

# 这种方式也可以实现卷挂载 如果构建时没有挂载卷，要手动镜像挂载 -v 卷名：容器内路径
```
### 数据卷容器
实现多个容器之间实现数据共享，利用父容器为其他容器实现数据共享
```bash
docker run -it --name docker01 dzg/centos:1.0
docker run -it --name docker02 --volumes-from docker01 dzg/centos:1.0 # 继承docker01的挂载目录
docker run -it --name docker03 dzg/centos:1.0
```
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