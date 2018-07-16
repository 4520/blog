---
layout: post
title: nvm 安装 node on linux
date: 2018-02-09 23:05:38
tags: ['nvm', 'node', 'npm']
---

![](https://blog.xlinyu.com/assets/images/2018-02-09/travel-3136679_1920.jpg)

	nvm 安装
	git clone https://github.com/creationix/nvm.git
	cd nvm 执行 ./install.sh
	安装之后输入nvm还是提示没有nvm这时候需要执行source ./nvm.sh
<!--more-->

	nvm安装任意版本nodejs
	1、通过nvm ls查看当前已经安装的node或者iojs版本；
	2、通过nvm ls-remote查看当前可以安装的node或者iojs版本；
	3、通过nvm install v8.0.0安装制定版本的nodejs；
	4、通过nvm use v8.0.0切换使用的nodejs版本；
上述完成后，就可以使用nvm管理node了，但是开启一个新的shell或重启机器后，会出现找不到node命令的情况。

	#设置默认的node
	$ nvm alias default v8.0.0

nvm 默认是从 http://nodejs.org/dist/ 下载的, 国外服务器, 必然很慢,
好在 nvm 以及支持从镜像服务器下载包, 于是我们可以方便地从淘宝的 node dist 镜像下载:

	$ NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node nvm install v8.0.0

于是你就会看到一段非常快速进度条:

	######################################################################## 100.0%
	Now using node v8.0.0

如果你不想每次都输入环境变量 NVM_NODEJS_ORG_MIRROR, 那么我建议你加入到 .bashrc 文件中:

	# nvm
	export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node
	source ~/.zshrc
	
	echo $NVM_NODEJS_ORG_MIRROR

![](https://blog.xlinyu.com/assets/images/2018-03-24/01.png)

**npm 设置为淘宝的源**

同理 nvm , npm 默认是从国外的源获取和下载包信息, 不慢才奇怪.
可以通过简单的 ---registry 参数, 使用国内的镜像 https://registry.npm.taobao.org :

	$ npm --registry=https://registry.npm.taobao.org install koa

**得到原本的镜像地址**
```shell	
$npm get registry 
> https://registry.npmjs.org/
$#设成淘宝的
$ npm config set registry http://registry.npm.taobao.org/
```
**换成原来的**

``` shell 
$ npm config set registry https://registry.npmjs.org/
```

