---
title: "python中string转换为datetime"
category: python
layout: post
tags: [python]
date: '2018-06-07 00:00:24'
---

python中将string转换为datetime类型比较简单。只要注意待转换字符串格式要跟正则表达式一致。另外还需要注意年月日的代表字母，比如年是```%Y```
```
from datetime import datetime
datetime_object = datetime.strptime('2018-04-26 11:30:00', '%Y-%m-%d %H:%M:%S')
print(type(datetime_object))
```
输出为：
```
<class 'datetime.datetime'>
```
