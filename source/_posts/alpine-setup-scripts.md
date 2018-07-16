---
layout: post
title: kickstart [unattended installation alpine]
date: 2018-03-25 15:36:12
tags: alpine
---

![](https://blog.xlinyu.com/assets/images/2018-03-25/03.jpg)

> https://netboot.xyz
>
> https://github.com/clandmeter/alpine-netboot
>
> https://github.com/gaulinux/MyLinuxSettings/blob/master/setup-alpine-answerfile
>
>https://wiki.alpinelinux.org/wiki/Alpine_setup_scripts
>
>https://github.com/sjiveson/nfs-server-alpine

<!--more-->

![setup-alpine](https://blog.xlinyu.com/assets/images/2018-03-25/setup-alpine.png)

```shell
➜  ~ setup-alpine -c ks.cfg
Answer file ks.cfg has been created.  Please add or remove options as desired in that file
 
 ➜  ~ cat ks.cfg
# Example answer file for setup-alpine script
# If you don't want to use a certain option, then comment it out

# Use US layout with US variant
KEYMAPOPTS="us us"

# Set hostname to alpine-test
HOSTNAMEOPTS="-n alpine-test"

# Contents of /etc/network/interfaces
INTERFACESOPTS="auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
    hostname alpine-test
"

# Search domain of example.com, Google public nameserver
DNSOPTS="-d example.com 8.8.8.8"

# Set timezone to UTC
TIMEZONEOPTS="-z UTC"

# set http/ftp proxy
PROXYOPTS="http://webproxy:8080"

# Add a random mirror
APKREPOSOPTS="-r"

# Install Openssh
SSHDOPTS="-c openssh"

# Use openntpd
NTPOPTS="-c openntpd"

# Use /dev/sda as a data disk
DISKOPTS="-m data /dev/sda"

# Setup in /media/sdb1
LBUOPTS="/media/sdb1"
APKCACHEOPTS="/media/sdb1/cache"


```
```shell
# 必须是绝对路径
# setup-alpine -f ~/ks.cfg

```





> 未完...
