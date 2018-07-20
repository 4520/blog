title: sts安装svn插件
date: 2018-07-20 09:41:33
tags: svn

本文介绍通过links的方式安装svn

![](http://arukas-blog.nos-eastchina1.126.net/assets/images/2018/07/20/64f020e8-c91c-49e9-8f74-c500c952091a.jpeg)

**下载地址**
svn已迁移到github,可以通过[github](https://github.com/subclipse/subclipse)下载源码自己构建,也可以通过本人上传的插件安装[subclipse-4.2.4.zip](http://arukas-blog.nos-eastchina1.126.net/assets/images/2018/07/20/subclipse-4.2.4.zip)

下载地址: https://dl.bintray.com/subclipse/releases/subclipse/

**解压后**

![svn解压](http://arukas-blog.nos-eastchina1.126.net/assets/images/2018/07/20/7898dde9-19ed-40ee-aa2e-ad1fbacd6f47.png)

<!--more-->

**安装步骤**

1. 在eclipse的安装目录eclipse中新建2个文件夹一般是myplugins和links
2. 在myplugins文件夹中新建一个文件夹命名为你需安装的插件名称我的是subclipse
3. 在subeclipse中再新建一个命名为eclipse的文件夹
4. 将插件压缩包解压出来有features和plugins这2个文件夹就把压缩包直接解压到eclipse文件夹中
5. 在eclipse的安装目录，新建一个命名为插件的文件，文件后缀为.link  我的为subclipse.link
6. 编辑subeclipse.link，在里面写svn的路径  文字内容为：``path=./myplugins/subclipse``
7. 重启eclipse,查看show view里有插件选项了   大功告成

![效果图](http://arukas-blog.nos-eastchina1.126.net/assets/images/2018/07/20/769ab8e7-e498-4684-b7ee-3cf6ceff35fb.png)
