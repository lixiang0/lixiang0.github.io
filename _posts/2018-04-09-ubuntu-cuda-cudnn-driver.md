---
title: "Ubuntu16.04下如何安装显卡驱动、cuda、cudnn"
category: other
layout: post
tags: [other,ubuntu]
date: '2018-04-09 14:50:24'
---

本文介绍如何在ubuntu16.04上安装nvidia显卡驱动以及cuda和cudnn。

其中nividia显卡的版本为最新版本
cuda为9.1版本
cudnn为7.1版本

介绍具体的过程。

## 1.安装显卡驱动
添加软件源：
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install nvidia-current
```
查看安装信息：
```
lsmod | grep nvidia 
```
如果需要移除驱动，执行：
```
sudo apt-get purge nvidia*
```
如果需要移除软件源，执行：
```
sudo apt-add-repository --remove ppa:graphics-drivers/ppa
```

## 2.获取cuda和cudnn

获取安装文件有两种方式：
一种是去管网下载cuda和cudnn。
链接如下：
```
https://developer.nvidia.com/cuda-downloads
https://developer.nvidia.com/cudnn
```
第二种这里给出百度网盘的链接：
```
链接: https://pan.baidu.com/s/12H3yDwr_JCcGi6nuEJ1Ikg 密码: fdkz
```
## 3.## 2.安装cuda和cudnn
安装的方式比较简单，下载了安装包之后直接安装即可：
```
sudo dpkg -i cuda-repo-ubuntu1604-9-1-local_9.1.85-1_amd64
sudo apt-key add /var/cuda-repo-9-1-local/7fa2af80.pub
sudo apt-get update
sudo apt-get install cuda
sudo dpkg -i libcudnn7_7.1.1.5-1+cuda9.1_amd64.deb
```
最后，别忘了设置一下环境变量：
```
export LD_LIBRARY_PATH=/usr/local/cuda/lib
export PATH=$PATH:/usr/local/cuda/bin
```
