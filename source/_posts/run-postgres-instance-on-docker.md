---
layout: post
title: 在docker上运行postgres实例
date: 2018-02-07 16:36:37
tags: postgres
---



![postgres](https://blog.xlinyu.com/assets/images/2018-02-07/2015011809283211487.jpg)

docker image直接从docker hub [官网](https://hub.docker.com/_/postgres/)获取，这里选用alpine的系统，image比较小``postgres:10.1-alpine``

```shell
➜  ~ docker pull postgres:10.1-alpine
➜  ~ docker run -d --name pg -p 5432:5432 -e POSTGRES_PASSWORD=pg  postgres:10.1-alpine
```

<!-- more -->

**容器状态**

```
➜  ~ docker ps
CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS              PORTS                    NAMES
0c798e446cbe        postgres:10.1-alpine   "docker-entrypoint..."   15 minutes ago      Up 15 minutes       0.0.0.0:5432->5432/tcp   pg
➜  ~ 
```

**pgAdmin连接数据库**

![postgres](https://blog.xlinyu.com/assets/images/2018-02-07/20180207165109.png)

> postgres镜像默认的用户名为`postgres`
>
> 登陆口令为创建容器是指定的值。



