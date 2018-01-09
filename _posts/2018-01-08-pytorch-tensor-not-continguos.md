---
title: "解决RuntimeError: input is not contiguous问题"
category: dl
layout: post
tags: [Pytorch,dl]
date: '2018-01-09 14:10:24'
---




出现了这个问题是因为tensor在内存中地址不是连续的，因而需要调用.contiguous()方法使得变为连续.


用法:

```
tensor_variable.contiguous()
```
