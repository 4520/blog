---
layout: post
title: install-docker-on-alpine-linux
date: 2018-03-24 19:46:23
tags: docker alpine
---

![docker on alpine linux](https://blog.xlinyu.com/assets/images/2018-03-25/01.jpg)

> http://wiki.alpinelinux.org/wiki/Docker



```shell
# 删除旧版本的docker
➜  ~ apk del docker
➜  ~  rm -rf /etc/docker /var/lib/docker /var/run/docker
```

<!--more-->

```shell
# 如果没有docker的安装包，需要将community地址添加到 /etc/apk/repositories 
➜  ~ apk add docker
(1/8) Installing libmnl (1.0.4-r0)
(2/8) Installing jansson (2.10-r0)
(3/8) Installing libnftnl-libs (1.0.8-r1)
(4/8) Installing iptables (1.6.1-r1)
(5/8) Installing libltdl (2.4.6-r4)
(6/8) Installing libseccomp (2.3.2-r1)
(7/8) Installing docker (17.12.1-r0)
Executing docker-17.12.1-r0.pre-install
(8/8) Installing docker-zsh-completion (17.12.1-r0)
Executing busybox-1.27.2-r8.trigger
OK: 710 MiB in 65 packages

# 启动服务
➜  ~ rc-service docker start
 * /var/log/docker.log: creating file
 * /var/log/docker.log: correcting mode
 * /var/log/docker.log: correcting owner
 * Starting docker ...                                                                                                         [ ok ]
# 验证服务是否启动 
# 也可以
# docker info 
➜  ~ docker version
Client:
 Version:       17.12.1-ce
 API version:   1.35
 Go version:    go1.9.4
 Git commit:    9584b2309e
 Built: Wed Mar  7 13:17:02 2018
 OS/Arch:       linux/amd64

Server:
 Engine:
  Version:      17.12.1-ce
  API version:  1.35 (minimum version 1.12)
  Go version:   go1.9.4
  Git commit:   v17.12.1-ce
  Built:        Wed Mar  7 13:16:22 2018
  OS/Arch:      linux/amd64
  Experimental: false
➜  ~ rc-update add docker boot
 * service docker added to runlevel boot

# 服务启动加载的脚本
➜  ~ rc-service -r docker
/etc/init.d/docker
```

**开启远程api及配置国内镜像**

```shell
➜  ~ vim /etc/conf.d/docker
```
DOCKER_OPTS默认为空值
```shell
# /etc/conf.d/docker: config file for /etc/init.d/docker
  
# where the docker daemon output gets piped
# this contains both stdout and stderr. If  you need to separate them,
# see the settings below
#DOCKER_LOGFILE="/var/log/docker.log"

# where the docker daemon stdout gets piped
# if this is not set, DOCKER_LOGFILE is used
#DOCKER_OUTFILE="/var/log/docker-out.log"

# where the docker daemon stderr gets piped
# if this is not set, DOCKER_LOGFILE is used
#DOCKER_ERRFILE="/var/log/docker-err.log"

# where docker's pid get stored
#DOCKER_PIDFILE="/run/docker.pid"

# where the docker daemon itself is run from
#DOCKERD_BINARY="/usr/bin/dockerd"

# any other random options you want to pass to docker
DOCKER_OPTS="-H 0.0.0.0:2375 -H unix:///var/run/docker.sock --registry-mirror=http://xxxx.m.daocloud.io"

# disable grsecurity features
#disable_grsec="chroot_deny_chmod chroot_deny_mknod"
```

重启docker服务，可以远程telnet一下docker的2375端口试试

```shell
➜  ~ service docker restart
 * WARNING: you are stopping a boot service
 * Stopping docker ...                                                                                                         [ ok ]
 * Starting docker ...                                                                                                         [ ok ]
➜  ~ telnet 192.168.163.200 2375

HTTP/1.1 400 Bad Request
Content-Type: text/plain; charset=utf-8
Connection: close

400 Bad RequestConnection closed by foreign host
➜  ~ 
```







