---
layout: post
title: alpine linux 常用软件
date: 2018-03-25 20:53:02
tags: alpine
---

![常用工具](https://arukas-blog.nos-eastchina1.126.net/assets/images/2018/03/25/02.jpg)

```shell
# 首先学习关机命令
# reboot   #重启系统类似于shutdown -r now。
# halt     #关机类似于shutdown -h now。
# poweroff #关机

# telnet
➜  ~ which telnet
telnet not found
➜  ~ apk add busybox-extras
(1/1) Installing busybox-extras (1.27.2-r8)
Executing busybox-extras-1.27.2-r8.post-install
Executing busybox-1.27.2-r8.trigger
OK: 711 MiB in 66 packages
➜  ~ which telnet
/usr/bin/telnet
➜  ~ 
```

<!--more-->

```shell
# ab 命令
# apk add apache2-utils

# 安装service命令 
# service not found
# apk add openrc

# 清除历史痕迹
# rm -f $HISTFILE && exit
```

```shell
# rc-update add docker boot #增加一个服务
# rc-update del docker boot #删除一个服务

# rc-status  #检查默认运行级别的状态
# rc-status -a #检查所有运行级别的状态

# rc-service sshd start #启动一个服务。
# rc-service sshd stop  #停止一个服务。
# rc-service sshd restart  #重启一个服务。
# 或者下面的命令
# service sshd status
```

