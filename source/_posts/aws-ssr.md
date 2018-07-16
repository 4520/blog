---
layout: post
title: aws-ssr
date: 2018-02-26 20:12:09
tags: ['ssr', 'ss']
---

![ssr](https://blog.xlinyu.com/assets/images/2018-02-26/dear-2309801_1920.jpg)

使用孟买节点，感觉速度还可以 https://ap-south-1.console.aws.amazon.com/ec2/v2/home?region=ap-south-1#LaunchInstanceWizard:

<!--more-->

```
docker pull s0fx2/shadowsocks-rss-alpine

# 需要开放443端口，参数可以查看github，也可以手动指定
docker run -d --name ssr -it -p 443:443 s0fx2/shadowsocks-rss-alpine
```

