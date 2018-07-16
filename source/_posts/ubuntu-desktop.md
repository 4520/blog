---
layout: post
title: ubuntu 18.04 桌面美化
date: 2018-05-06 13:28:19
tags: ubuntu
---

![爆照](https://blog.xlinyu.com/assets/images/2018-05-06/success.png)

## 安装sshd

```bash
sudo apt-get install net-tools
sudo apt-get -y install openssh-server
service sshd status
systemctl status sshd
```
## 安装chrome

```bash
# Add Google Chrome Repository
sudo wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" | sudo tee /etc/apt/sources.list.d/google-chrome.list

# Install Google Chrome
sudo apt-get update

# To Install Google Chrome Stable, use the below command.
sudo apt-get -y install google-chrome-stable

# activities or terminal
google-chrome
```

<!--more-->

## 配置国内源

```bash
# https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/
sudo mv /etc/apt/sources.list /etc/apt/sources.list.bak
sudo vim /etc/apt/sources.list
# add 
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse


```

## Themes

> https://www.cnblogs.com/feipeng8848/p/8970556.html

```bash
sudo apt install gnome-tweak-tool
sudo apt install chrome-gnome-shell
sudo apt install gnome-shell-extensions

sudo apt install docky
mkdir ~/.themes
mkdir ~/.icons

git clone https://github.com/harshp2035/Gnome-OSX.git --depth=1

# icons
git clone https://github.com/keeferrourke/la-capitaine-icon-theme.git --depth=1
git clone https://github.com/Hikari9/MacBuntu-OS-Icons MacBuntu-OS

# install dash dock
https://github.com/micheleg/dash-to-dock

```

## zsh

```bash
# Via curl
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# Via wget
# sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"


# 手动安装
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh 

cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

# ubuntu linux
sudo usermod -s /bin/zsh $USER


```

