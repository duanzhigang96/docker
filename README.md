# docker
learn docker


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
