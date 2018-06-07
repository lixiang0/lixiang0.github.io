---
title: "python中UnicodeDecodeError：'gb2312'codec can't decode bytes：illegal multibyte sequence解决办法"
category: other
layout: post
tags: [python]
date: '2018-06-07 00:00:25'
---

当使用```bytes.decode("gb2312")```是出现题述问题。

出现这个问题的原因是处理的字符中夹杂特殊字符是gb2312字符集中没有的，因而只需要使用更大一点的字符集```GB18030```去解析即可。

另外GB2312，gbk，gb18030字符集大小顺序为：GB2312 < GBK < GB18030
