---
title: "Python中的装饰器"
category: python
layout: post
tags: [python]
date: '2019-11-12 14:00:24'
---

有时候在看python源码的时候会看到在方法上面有个@的标识，这就是是装饰器。
装饰器提供了一种修改方法或类的灵活性，可以在不改变或者不必了解方法或者类的内部实现的基础上修改方法或者类。
比如：
```
from flask import Flask
app=Flask(__name__)

@app.route('/')
def hello():
    return 'hello'
```

上述代码表示hello方法以及参数'/'需要传入@声明的方法app.route()执行。

等同于
```
rule      = "/"
view_func = hello
# They go as arguments here in 'flask/app.py'
def add_url_rule(self, rule, endpoint=None, view_func=None, **options):
    pass
```
