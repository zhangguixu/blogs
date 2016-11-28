---
title: ubuntu安装中文输入法
date: 2016-11-28 18:36:32
categories:
    - linux
tags:
    - 输入法
---

环境： ubuntu 14.01 英文系统
操作： 安装fcitx和中文输入法

<!-- more -->

## 1. 安装fcitx

打开软件下载中心，搜索fcitx，安装fcitx

![fcitx-01](/uploads/fcitx-01.png)

## 2. 切换输入

1. 打开bash，输入input，打开input method

    ![fcitx-02](/uploads/fcitx-02.png)

2. 一直进行下一步，直到

    ![fcitx-03](/uploads/fcitx-03.png)

3. 然后点击直到结束，之后重启电脑，就可以看到

    ![fcitx-04](/uploads/fcitx-04.png)

## 2. 安装搜狗拼音

下载[搜狗拼音的linux](http://pinyin.sogou.com/linux/?r=pinyin)

下载之后点击安装既可，之后就可以看到搜狗输入法

![fcitx-05](/uploads/fcitx-05.png)

## 3. 安装googlepinyin

搜狗输入法有时候会有点问题，个人还是喜欢googlepinyin

安装了fcitx之后，再安装googlepinyin

```shell
sudo apt-get install fcitx-googlepinyin
```

之后可以在有上方的输入法中点击配置，新添我们安装的谷歌输入法

![fcitx-06](/uploads/fcitx-06.png)