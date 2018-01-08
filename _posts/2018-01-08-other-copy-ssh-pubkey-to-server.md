---
title: "如何添加新的pub key到远程服务器"
category: other
layout: post
tags: [other,ssh]
date: '2018-01-06 17:00:24'
---


在新的机器上使用git提交代码或者ssh登陆远程服务器的时候往往需要远程服务器密码，或者在远程服务器添加ssh的pub key。

那么如何在本地直接将pub key拷贝到远程服务器，从而实现免密登陆呢？

有两种办法：

第一种方法：

```
#将本地id_rsa.pub复制到远程服务器
scp ~/.ssh/id_rsa.pub ruben@cpp.pub:/tmp/id_rsa.pub
#下面的步骤在服务器上操作
ssh ruben@cpp.pub
cat /tmp/id_rsa.pub >> ~/.ssh/authorized_keys

```


第二种方法（以我的服务器为例）：

```

ssh-copy-id ruben@cpp.pub

```


完成以上操作就可以直接在本地免密直接登陆远程主机或者使用git提交代码了。
