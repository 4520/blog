---
layout: post
title: Ubuntu安装Jdk–大Java走起
date: 2018-02-06 22:37:15
tags: ['java', 'jdk']
---

![大java走起](https://blog.xlinyu.com/assets/images/2018-02-06/2015011811124013974.jpg)

**下载java8的最新版本**

```shell
$ 两种方式下载
$ curl -L "http://download.oracle.com/otn-pub/java/jdk/8u172-b11/a58eab1ec242421181065cdc37240b08/jdk-8u172-linux-x64.tar.gz" -H "Cookie: oraclelicense=accept-securebackup-cookie"  -H "Connection: keep-alive" -O  

$ wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u172-b11/a58eab1ec242421181065cdc37240b08/jdk-8u172-linux-x64.tar.gz
```

<!-- more -->

解压到指定的目录

```shell
$ sudo tar -zxvf jdk-8u172-linux-x64.tar.gz -C /opt
$ sudo ln -s /opt/jdk1.8.0_172 /opt/java 
```

**配置环境变量**

```shell
$ sudo vim /etc/profile
```

![配置环境变量](https://blog.xlinyu.com/assets/images/2018-02-06/20180206234949.png)

```shell
# env
export JAVA_HOME=/opt/java
export CLASSPATH=.:$JAVA_HOME/jre/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$HOME/bin:$JAVA_HOME/bin
```
使环境变量生效

```shell
$ source /etc/profile
```

查看jdk版本

![java -version](https://blog.xlinyu.com/assets/images/2018-02-06/20180206235648.png)
