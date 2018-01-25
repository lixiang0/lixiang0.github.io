---
title: "Ubuntu下安装dlib"
category: other
layout: post
tags: [other,ubuntu]
date: '2018-01-25 14:20:24'
---

本文介绍dlib在ubuntu系统中的安装方法。

在安装之前首先要确定python3已经安装。

### 安装依赖包和下载代码：

```
sudo apt-get install libboost-all-dev
git clone https://github.com/davisking/dlib.git
```

### 编译C++ so库

```
cd dlib
mkdir build
cd build
cmake .. -DDLIB_USE_CUDA=0 -DUSE_AVX_INSTRUCTIONS=1
cmake --build .
```

### 安装python模块

```
cd ..
python3 setup.py install --yes USE_AVX_INSTRUCTIONS --no DLIB_USE_CUDA
```

完毕～
