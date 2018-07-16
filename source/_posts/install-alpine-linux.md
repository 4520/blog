---
layout: post
title: 安装Alpine Linux
date: 2018-02-08 15:58:17
tags: alpine
---

![](https://blog.xlinyu.com/assets/images/2018-02-08/201501172300446668.jpg)

**下载iso**

[下载地址](https://alpinelinux.org/downloads/)，创建vmware虚拟机，挂载下载的image.启动就进入登录界面了。用户名root，密码是空。（默认的）,根据提示

<!-- more -->

**setup-alpine**

![setup-alpine](https://blog.xlinyu.com/assets/images/2018-02-08/install/setup-alpine.png)

**键盘布局**

![keyboard-layout](https://blog.xlinyu.com/assets/images/2018-02-08/install/keyboard-layout.png)

**hostname**

根据实际情况，一般默认既可

**网卡配置**

默认既可以

**ip地址配置**

可以使用dhcp，我这里使用static

```shell
ip: 192.168.163.200
netmask: 255.255.255.0
gateway: 192.168.163.2

## 也可以安装完后手动修改
# vim /etc/network/interfaces
# like this

auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
        address 192.168.163.200
        netmask 255.255.255.0
        gateway 192.168.163.2


# 也可以通过setup设置
# https://wiki.alpinelinux.org/wiki/Alpine_setup_scripts
alpine:/bin# setup-
setup-acf              setup-bootable         setup-hostname         setup-mta              setup-timezone
setup-alpine           setup-disk             setup-interfaces       setup-ntp              setup-xen-dom0
setup-apkcache         setup-dns              setup-keymap           setup-proxy            setup-xorg-base
setup-apkrepos         setup-gparted-desktop  setup-lbu              setup-sshd
```

![ip-config](https://blog.xlinyu.com/assets/images/2018-02-08/install/ip-config.png)

**配置dns、root密码**

![dns](https://blog.xlinyu.com/assets/images/2018-02-08/install/dns.png)

**时区配置**

``Asia/Shanghai``

**选择image**

r: 随机的

f: 在已有的选择最快的

e: 手动修改配置文件

也可以在系统安装完后修改

![mirror](https://blog.xlinyu.com/assets/images/2018-02-08/install/mirror.png)

**ssh server**

服务器一般会选择安装的，默认即可

![sshserver](https://blog.xlinyu.com/assets/images/2018-02-08/install/sshserver.png)

**NTP默认既可**

**格式化硬盘**

![format](https://blog.xlinyu.com/assets/images/2018-02-08/install/format.png)

**重启alpine linux**

```shell
# reboot
```

**开启root远程登陆**

默认配置

![default-ssh](https://blog.xlinyu.com/assets/images/2018-02-08/install/default-ssh.png)

修改后配置

![root-ssh](https://blog.xlinyu.com/assets/images/2018-02-08/install/root-ssh.png)

```shell
# service sshd restart
# ssh localhost
```
**国内镜像配置**

```shell
# vi /etc/apk/repositories
#/media/cdrom/apks
#http://dl-cdn.alpinelinux.org/alpine/v3.7/main
#http://dl-cdn.alpinelinux.org/alpine/v3.7/community

#http://dl-cdn.alpinelinux.org/alpine/edge/main
#http://dl-cdn.alpinelinux.org/alpine/edge/community
#http://dl-cdn.alpinelinux.org/alpine/edge/testing
# 清华mirror
https://mirror.tuna.tsinghua.edu.cn/alpine/v3.7/main
https://mirror.tuna.tsinghua.edu.cn/alpine/v3.7/community


# 更新源信息
# apk add --update
```

```shell
# 防火墙的配置
# /etc/init.d/iptables save

```




> https://wiki.alpinelinux.org/wiki/Main_Page
>
> https://wiki.alpinelinux.org/wiki/Alpine_setup_scripts
>
> https://www.youtube.com/watch?v=1G4nmUUk2kI
>
> https://mp.weixin.qq.com/s?__biz=MzI2MDY5Mzc0Ng==&mid=2247483953&idx=1&sn=c0790b2d73bcd047f8a84d604fc24a8a&chksm=ea6489acdd1300ba092c85b54ccecb417e3c28127ec9a7c280325af4b8737b74c29888c2081a#rd





