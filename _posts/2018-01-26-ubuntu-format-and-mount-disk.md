---
title: "Ubuntu下格式化和挂载硬盘"
category: other
layout: post
tags: [other,ubuntu]
date: '2018-01-26 20:20:24'
---

本文介绍如何在ubuntu下格式化和挂载硬盘。

首先执行```df -h```命令查看系统的硬盘找到类似下面形式的盘符：
```
/dev/sda1       910G  708G  156G  82% /
```

硬盘在系统中显示为```/dev/sda0```或```/dev/sdb1```之类。比如上面的就表示```/dev/sda0```作为```/```跟目录。

然后执行```sudo mkfs -t ext4 /dev/sdb````命令格式化硬盘。

最后挂载：
```
mkdir ~/data
sudo mount /dev/sdb` ~/data
```
上述操作将```/dev/sdb1```映射到```~/data```目录。

