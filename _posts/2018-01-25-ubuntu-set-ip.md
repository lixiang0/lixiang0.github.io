---
title: "Ubuntu命令行下设置IP"
category: other
layout: post
tags: [other,ubuntu]
date: '2018-01-25 21:20:24'
---

本文介绍通过命令行设置IP、网关的方法。
首先通过```ifconfig```命令查看系统的网卡。
比如本文使用的网卡是```eth1```。
然后通过下面的命令设置IP和网关。

```
sudo ifconfig eth0 172.16.1.226 netmask 255.255.255.0
sudo route add default gw 172.16.1.1 eth0
```

重启网络服务：
```
sudo /etc/init.d/networking restart
```

查看路由情况：

```
route -n
```
