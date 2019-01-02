---
title: "github中遇到>100MB文件的解决办法"
category: other
layout: post
tags: [问题]
date: '2019-01-02 14:00:25'
---

今天在GitHub上传文件时遇到文件大于>100MB文件的错误，如下：
```
GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
```

因GitHub不支持大于100MB文件的问题，解决的办法就是从commit中移除该文件：
```
git filter-branch -f --index-filter 'git rm --cached --ignore-unmatch >100MB_file_name'
```

运行之后再继续执行```git push```即可。
