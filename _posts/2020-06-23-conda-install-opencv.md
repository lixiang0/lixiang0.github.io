---
title: "conda无法安装opencv的解决办法"
category: other
layout: post
tags: [other]
date: '2020-06-23 11:00:24'
---

在新电脑中用conda命令安装opencv，但不是403错误就是超时。错误如下：
```
Collecting package metadata (repodata.json): done
Solving environment: failed
Initial quick solve with frozen env failed.  Unfreezing env and trying again.
Solving environment: failed
```
解决的办法是使用pip安装：```pip install opencv-python```即可解决。
