---
title: "如何开启jupyter的远程服务"
category: other
layout: post
tags: [other,jupyter]
date: '2018-01-08 15:00:24'
---

本文介绍如何开放jupyter的远程功能。

### 设置jupyter notebook密码：

```
jupyter notebook password
```
可以看到如下输出：

```
Enter password: 
Verify password: 
[NotebookPasswordApp] Wrote hashed password to /home/yyddl/.jupyter/jupyter_notebook_config.json
```

### 修改配置文件
执行：

```
cat ~/.jupyter/jupyter_notebook_config.json
#上面的命令会输出经过hash的密码，下面的步骤会用到。

jupyter notebook --generate-config

vim ~/.jupyter/jupyter_notebook_config.py
```

修改：

```

## The IP address the notebook server will listen on.
c.NotebookApp.ip = '0.0.0.0'

#  The string should be of the form type:salt:hashed-password.
c.NotebookApp.password = 'sha1:3573e878e007:ebebac2259023ba.....'
```

到这里就完成了基本的配置了。

之后通过：
```
jupyter notebook
```
打开浏览器界面，输入密码即可编码了~


