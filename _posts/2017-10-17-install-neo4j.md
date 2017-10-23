---
title: "[neo4j]1.Install Neo4j"
catagories: neo4j
layout: post
date: '2017-10-17 21:00:24'
---


### 1.下载[neo4j](https://neo4j.com/artifact.php?name=neo4j-community-3.2.6-unix.tar.gz)
![]({{ "/imgs/20171023-210216.png" | absolute_url }})
### 2.解压运行：
```
sudo ./bin/neo4j console
```
![]({{ "/imgs/20171023-210234.png" | absolute_url }})
### 3.
打开浏览器：http://localhost:7474/browser/（默认账户密码：neo4j neo4j）
![]({{ "/imgs/20171023-210309.png" | absolute_url }})
### 4.
自带电影的例子（点击Favorities->Get some data->右上角Run按钮）
![]({{ "/imgs/20171023-210427.png" | absolute_url }})
### 额外
下载[驱动](https://pypi.python.org/pypi/neo4j-driver)
.安装：
```
python3 setup.py install
```