---
title: "fatal error:opencv2/highgui/highgui_c.h:No such file or directory"
category: other
layout: post
tags: [other]
date: '2018-10-23 14:37:24'
---

在编译yolo v3的时候遇到错误：

```
include/darknet.h:25:43: fatal error: opencv2/highgui/highgui_c.h: No such file or directory
```
但已经通过conda安装了opencv了

想想应该是有的系统lib之类的没装，解决办法如下,命令行执行： 

```
sudo apt-get install libopencv-dev
```

即可
