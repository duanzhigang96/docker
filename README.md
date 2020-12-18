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
```
