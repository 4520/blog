---
layout: post
title: git常用命令
date: 2018-02-26 19:18:04
tags: git
---

![git](https://blog.xlinyu.com/assets/images/2018-02-26/elephant-3177249_1920.jpg)

<!--more-->

```
## 删除本地分支
git branch -d branch-name	#删除已合并分支
git branch -D branch-name	#删除未merge的分支


## 删除远程分支
git branch -r -d origin/branch-name
git push origin :branch-name
# 直接删除远程分支 Git v1.7.0后，支持这种语法
git push origin --delete <branchName>

## 显示远程仓库
git remote show origin
```





