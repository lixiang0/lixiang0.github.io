---
title: "ssh “permissions are too open” error"
category: other
layout: post
tags: [other]
date: '2021-01-10 00:00:24'
---

出现这个问题是因为```~/.ssh/id_rsa```文件的权限给的太宽。

如果有这个提示，可以使用命令使得文件只有读权限：

```
chmod 400 ~/.ssh/id_rsa
```

或者如果需要添加写权限

```
chmod 600 ~/.ssh/id_rsa
```

完毕。

