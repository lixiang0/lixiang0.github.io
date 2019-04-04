---
title: "解决Python bottle module Error: 413 Request Entity Too Large问题"
category: other
layout: post
tags: [问题]
date: '2019-04-04 14:01:25'
---

服务器使用了bottle，通过http的post方法上传图片，收到如下错误：
```
Error: 413 Request Entity Too Large
```

解决的办法就是修改文件的大小上限：
```
import bottle
bottle.BaseRequest.MEMFILE_MAX = 1024 * 1024 # (or whatever you want)
```
即可

