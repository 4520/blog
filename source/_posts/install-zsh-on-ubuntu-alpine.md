---
layout: post
title: install zsh on ubuntu or alpine
date: 2018-02-09 22:38:11
tags: ['zsh', 'bash', 'shell']
---

![](https://blog.xlinyu.com/assets/images/2018-02-09/seashell-3043735_1920.jpg)

> 官网地址：[https://ohmyz.sh/](https://ohmyz.sh/)
>
> wiki: [https://github.com/robbyrussell/oh-my-zsh/wiki](https://github.com/robbyrussell/oh-my-zsh/wiki)

<!-- more -->

**安装zsh**

```shell
# ubuntu linux
$ sudo apt-get install -y zsh curl wget git

# alpine linux
# apk add zsh curl wget git
```

**参照官网**

```shell
# Via curl
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# Via wget
# sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

![](https://blog.xlinyu.com/assets/images/2018-02-09/20180209224814.png)

**改变当前用户的shell**

```shell
# ubuntu linux
$ sudo usermod -s /bin/zsh $USER
$ exit

# alpine linux
# sed -i -e "s/bin\/ash/bin\/zsh/" /etc/passwd
# exit
```

**重新登陆shell**

![](https://blog.xlinyu.com/assets/images/2018-02-09/20180209225531.png)

### 关于环境变量的问题

> [https://superuser.com/questions/41290/system-wide-environment-variables-for-zsh-on-ubuntu](https://superuser.com/questions/41290/system-wide-environment-variables-for-zsh-on-ubuntu)
>
> The manual page zsh(1) states that zsh reads /etc/zsh/zprofile. You could simply add a command there 
>
> which sources /etc/profile
>
> $ sudo vim /etc/zsh/zprofile
>
> \# add source
>
> source /etc/profile
>
> exit
>
> login
>
> ok.....very tanks