---
title: "解决Ubuntu下pip3安装TA-Lib失败的问题"
category: other
layout: post
tags: [other,ubuntu]
date: '2019-07-01 17:20:24'
---
在ubuntu系统下安装TA-Lib遇到了如下问题：
```
talib/_ta_lib.c:526:28: fatal error: ta-lib/ta_defs.h: No such file or directory
```

解决办法：
```
wget http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz
tar -zxf ta-lib-0.4.0-src.tar.gz
cd ta-lib/
./configure --prefix=/usr
make
sudo make install
pip3 install ta-lib
```

即可～
