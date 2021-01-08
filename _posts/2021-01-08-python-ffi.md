---
title: "fatal error: ffi.h: No such file or directory问题的解决"
category: python
layout: post
tags: [other,python]
date: '2018-01-26 00:00:24'
---

For Debian and Ubuntu:

```$ sudo apt-get install build-essential libssl-dev libffi-dev python-dev```

For Fedora and RHEL-derivatives:

```$ sudo yum install gcc libffi-devel python-devel openssl-devel```

For Alpine Linux: 
```libffi-dev, openssl-dev and python3-dev```
