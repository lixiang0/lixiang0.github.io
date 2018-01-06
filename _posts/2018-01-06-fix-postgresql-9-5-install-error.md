---
title: "解决postgresql 9.5安装失败的问题"
category: other
layout: post
tags: [postgresql,问题]
date: '2018-01-06 14:00:24'
---

在低版本的Ubuntu系统中安装postgresql 9.5遇到下面的问题：

```
E: Unable to locate package postgresql-9.5
```

原因是因为低版本中只支持到9.3所以需要手动的更新source list。

解决方案为依次运行：

```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main 9.5" >> /etc/apt/sources.list.d/postgresql.list'
sudo apt-get update
sudo apt-get install postgresql-9.5
```
