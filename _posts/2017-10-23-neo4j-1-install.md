---
title: "1.Install Neo4j"
category: kg
layout: post
tags: [neo4j,kg]
date: '2017-10-17 21:00:24'
---


### 1.下载[neo4j](https://neo4j.com/artifact.php?name=neo4j-community-3.2.6-unix.tar.gz)
![]({{ "/imgs/20171023-210216.png" | absolute_url }})

### 2.解压之后运行：
```
sudo ./bin/neo4j console
```

<img src="/imgs/20171023-210234.png" alt="Smiley face" height="250">

### 3.登录后台
打开浏览器：http://localhost:7474/browser/（默认账户密码：neo4j neo4j）

<img src="/imgs/20171023-210309.png" alt="Smiley face" height="250">

### 4.运行自带的示例

自带电影的例子（点击Favorities->Get some data->右上角Run按钮）

<img src="/imgs/20171023-210427.png" alt="Smiley face" height="400">

### 5.添加python支持

安装[python驱动](https://pypi.python.org/pypi/neo4j-driver)：
```
pip install neo4j
```
