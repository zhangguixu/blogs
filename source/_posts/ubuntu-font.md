---
title: ubuntu安装微软雅黑字体
date: 2016-11-28 18:47:08
categories:
    - linux
tags:
    - 字体
---

环境： ubuntu 14.01 英文系统
操作： 安装微软雅黑字体

<!-- more -->

## 具体步骤

首先在window下的c://window/Fonts 中找出`msyh.ttc`和`msya.ttf`(最好是将所有关于msyh的)，将其拷贝出来

切换到ubuntu下，我们可以在/usr/share/fonts下创建一个文件夹，用于放置这个字体文件

```shell
cd /usr/share/fonts
sudo mkdire winfonts
```

之后将该字体文件拷贝到winfonts中，改变字体文件的访问权限，在winfonts文件夹下执行

```shell
sudo chmod 744 *
```

然后根据字体文件生成核心字体信息

```shell
sudo mkfontscale
sudo mkfontdir
sudo fc-cache -fv
```

之后注销一下即可。

接下来，就是要使用我们导入的微软字体，可以在软件中心搜索unity tweak tool，然后安装

![font-01](/uploads/font-01.png)

之后打开软件，就可以进入font选项

![font-02](/uploads/font-02.png)

然后就可以设置

![font-03](/uploads/font-03.png)