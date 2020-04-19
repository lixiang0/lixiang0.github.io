---
title: "解决Bottle中的CORS问题"
category: python
layout: post
tags: [python]
date: '2020-04-19 14:00:24'
---

最近在将安全帽检测算法发布到web上，网页中需要通过http post方法访问其他服务器的IP，执行操作的时候出现```from origin 'null' has been blocked by CORS policy```错误。

原因是：web server为了保证安全禁止了资源的跨域访问。

解决办法：

首先google了一些解决办法，试了下发现没有起作用，最后发现是因为网络上的解决办法的bottle版本是老版本，新版本有些规则变了。

所以本文就列出最新版本的解决办法。

解决的办法也简单，只需要给header添加'Access-Control-Allow-Origin'='*'即可。参考如下代码：
```
@route("/upload", method=['POST'])
def hello():
    bottle.response.set_header('Access-Control-Allow-Origin', '*')
    bottle.response.add_header('Access-Control-Allow-Methods',
                        'GET, POST, PUT, OPTIONS')
    bottle.response.add_header('Access-Control-Allow-Headers',
                        'Origin, Accept, Content-Type, X-Requested-With, X-CSRF-Token')
```

另外需要注意的是，bottle中@route("/upload", method=['POST'])中method中不支持list的写法，如果同时支持POST和GET方法需要分开两行写。
如下：
```
@route("/upload", method=['POST'])
@route("/upload", method=['GET'])
def hello():
  pass
```
