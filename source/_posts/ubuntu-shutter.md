---
title: ubuntu安装截图软件shutter
date: 2016-11-28 18:54:12
categories:
  - linux
tags:
  - 截图软件
---

环境： ubuntu 14.01 英文系统
操作： 安装截图软件shutter，并且设置截图的快捷键

<!-- more -->

## 1. 添加软件源并安装

*如果没有添加，安装的shutter不是截图工具*

```shell
sudo add-apt-repository ppa:shutter/ppa
sudo apt-get update
sudo apt-get install shutter
```

安装成功后，在bash中搜索shutter

![shutter-01.png](/uploads/shutter-01.png)

## 2. 设置快捷键

1. 打开系统设置

    ![shutter-02.png](/uploads/shutter-02.png)

2. 打开keyboard键盘设置

    ![shutter-03.png](/uploads/shutter-03.png)

3. 添加成功之后，设置快捷键

    ![shutter-04.png](/uploads/shutter-04.png)

4. 单击右侧Disabled，然后快速按下ctrl+alt+a

## 3. 使用

1. 按下快捷键ctrl+alt+a，然后选择要截图的区域，之后双击，就会出现

    ![shutter-05.png](/uploads/shutter-05.png)

2. 这个时候已经截图成功了，我们可以进行进一步的编辑，点击edit,即可编辑

    ![shutter-06.png](/uploads/shutter-06.png)
