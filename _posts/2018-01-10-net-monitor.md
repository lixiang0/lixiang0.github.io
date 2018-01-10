---
title: "Ubuntu下的网络监控"
category: other
layout: post
tags: [other,ubuntu]
date: '2018-01-10 21:00:24'
---
Nethogs 是一个终端下的网络流量监控工具，它的特别之处在于可以显示每个进程的带宽占用情况，这样可以更直观获取网络使用情况。

使用方法：
```
sudo apt-get install nethogs #安装工具
sudo nethogs eth0 #或者eth1 ifconfig查看系统的网卡

```


<img src="/imgs/2018-01-10-21-30-44.png" alt="Smiley face" height="130">
