列出所有镜像
```
docker images -a
```
只显示镜像id
```
docker images -q
```

查看运行中的容器
```
docker ps
```

开启某个docker
```
docker start CONTAINER_ID
```

在docker hub里查找STARS大于3000的mysql相关的镜像
```
docker search mysql --filter=STARS=3000
```

下载镜像
```
docker pull img_name:tag
# 分层下载
```

删除镜像
```
docker rmi -f ${docker images -aq} # del all
docker rmi -f ${CONTAINER_ID} # del all
```


## docker run

```
xhost local:root
docker run -p 9001:22 -it  --privileged   -e DISPLAY=$DISPLAY   -v C:\Users\94806\Downloads:/data   ubuntu-eprosima-dds-suite:v1.3.0
```