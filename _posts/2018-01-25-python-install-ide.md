---
title: "Ubuntu下Virtualbox添加usb支持"
category: other
layout: post
tags: [other,ubuntu]
date: '2018-01-25 14:00:24'
---

在宿主机上安装了一个免驱摄像头，但是想要在虚拟机中使用的话应该怎么办呢？

方法很简单：

首先下载打开virtualbox的[下载地址](https://www.virtualbox.org/wiki/Downloads),找到支持插件[VirtualBox Extension Pack下载链接](https://download.virtualbox.org/virtualbox/5.2.6/Oracle_VM_VirtualBox_Extension_Pack-5.2.6-120293.vbox-extpack)
。

下载到本地之后双击即可。注意要先将已经打开的虚拟机关闭。


安装成功之后，打开虚拟机，选择Device-->Webcams-->usb2.0 camera，即可在虚拟机中使用

在虚拟机命令行中执行```ls /dev/vide0```可以看到输出```/dev/video0```即表示安装成功。

如果想验证摄像头是否能正常使用可以安装camorama:```sudo apt-get install camorama```。然后命令行执行```camorama```即可～
