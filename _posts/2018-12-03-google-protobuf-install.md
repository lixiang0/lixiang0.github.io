---
title: "ubuntu中安装google protobuf"
category: other
layout: post
tags: [other]
date: '2018-12-03 18:00:24'
---

### 安装


```
$ sudo apt-get install autoconf automake libtool curl make g++ unzip
$ git clone https://github.com/protocolbuffers/protobuf.git
$ cd protobuf
$ git submodule update --init --recursive
$ ./autogen.sh
$ ./configure
$ make
$ make check
$ sudo make install
$ sudo ldconfig # refresh shared library cache.
```
