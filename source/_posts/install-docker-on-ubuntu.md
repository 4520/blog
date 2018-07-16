---
layout: post
title: install-docker-on-ubuntu
date: 2018-02-26 20:54:04
tags: docker
---

![dog](https://blog.niuyuxian.tk/assets/images/2018-02-26/dog-2449668_1920.jpg)

<!--more-->

参考docker官方文档

```
#删除旧版本
sudo apt-get remove docker docker-engine docker.io

sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common -y
    
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt-get update

sudo apt-get install docker-ce -y

sudo docker info
or
sudo systemctl status docker
```

**no sudo**

```
$ sudo usermod -aG docker $USER
$ eixt &&  login
```



## 国内加速

下面的加速器二选一

**阿里云加速器**

```
sudo mkdir -p /etc/systemd/system/docker.service.d

sudo tee /etc/systemd/system/docker.service.d/mirror.conf <<-'EOF'
[Service]
ExecStart=
ExecStart=/usr/bin/docker daemon -H fd:// --registry-mirror=https://1pdiorim.mirror.aliyuncs.com
EOF

sudo systemctl daemon-reload
sudo systemctl restart docker
```

**daocloud.io**

```
curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://d2c27e88.m.daocloud.io

sudo cat /etc/docker/daemon.json 
{"registry-mirrors": ["http://d2c27e88.m.daocloud.io"]}
```



## docker remote api

```
-------------------------
sudo vim /etc/default/docker
# 添加参数
DOCKER_OPTS='-H 0.0.0.0:6000 -H unix:///var/run/docker.sock'
 
sudo vim /lib/systemd/system/docker.service 
# 指定环境变量文件 
EnvironmentFile=/etc/default/docker
ExecStart=/usr/bin/dockerd -H fd:// $DOCKER_OPTS
-------------------------
# 重启服务
sudo systemctl daemon-reload
sudo systemctl restart docker

# 查看端口
ps -ef|grep  docker

参考: http://paper.seebug.org/354/
```