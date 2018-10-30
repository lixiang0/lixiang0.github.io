---
title: "如何更新ubuntu中cmake版本"
category: other
layout: post
tags: [other]
date: '2018-09-06 18:00:24'
---
在编译某些项目的时候发现对cmake的版本要求是3.11以上，但是通过update和upgrade的操作之后cmake的版本还是停留在3.5的状态，之后按照网上的一些方法依然没有成功。最后使用源码的方法安装成功了。具体的操作过程如下：
### 1.下载cmake

打开[cmake](https://cmake.org/download/)官网，或者直接点击
[cmake3.12-linux版本](https://cmake.org/files/v3.12/cmake-3.12.1.tar.gz)地址下载。

### 2.安装

注意本文使用的是3.12版本，在安装的时候使用跟自己下载的版本对应的本地路径。
```
tar -xvf cmake-3.12.1.tar.gz
cd cmake-3.12.1
cmake .
make -j8
sudo make install
```
### 3.更新

使用：
```
sudo update-alternatives --install /usr/bin/cmake cmake /usr/local/bin/cmake 1 --force
```

可以看到输出的是：
```
cmake version 3.12.1

CMake suite maintained and supported by Kitware (kitware.com/cmake).
```
即可~
