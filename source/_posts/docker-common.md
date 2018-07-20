---
layout: post
title: docker常用操作
date: 2018-02-26 22:15:54
tags: ['docker']
---

![docker](https://arukas-blog.nos-eastchina1.126.net/assets/images/2018/02/26/golden-gate-bridge-1596161_1920.jpg)



docker run -p 8761:8761 --net=host --rm --name e2 ncc0706/eureka-server 

**网络**

```
# 网桥工具
$ sudo apt-get install bridge-utils 
```

<!--more-->

> 参考：http://blog.csdn.net/gezhonglei2007/article/details/51627821

docker network所有子命令如下：

- docker network create
- docker network connect
- docker network ls
- docker network rm
- docker network disconnect
- docker network inspect
```
# 创建网卡
# docker network create --driver=bridge --subnet=10.10.0.0/16 --gateway=10.10.0.1 global
# docker network rm br-318641c175a7
# docker network inspect global
```

**容器不能连接宿主机**

可以通过--net=host方式启动容器

进入容器后查看路由：

```
/ # route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         192.168.163.2   0.0.0.0         UG    0      0        0 ens33
10.10.0.0       *               255.255.0.0     U     0      0        0 br-ee8e5538ff35
172.17.0.0      *               255.255.0.0     U     0      0        0 docker0
172.19.0.0      *               255.255.0.0     U     0      0        0 br-5e405eb8d81c
192.168.163.0   *               255.255.255.0   U     0      0        0 ens33

# 可以看到宿主机的ip信息
```

**none镜像删除**

```
docker ps -a | grep "Exited" | awk '{print $1 }'|xargs docker stop
docker ps -a | grep "Exited" | awk '{print $1 }'|xargs docker rm
docker images|grep none|awk '{print $3 }'|xargs docker rmi
```
