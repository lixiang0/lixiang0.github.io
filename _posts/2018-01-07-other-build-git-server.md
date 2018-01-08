---
title: "如何搭建自己的GIT服务器"
category: other
layout: post
tags: [git,other]
date: '2018-01-07 14:00:24'
---

基本上的程序员都会有一个自己github帐号,帐号下都有若干个项目.有些项目适合公开,有些项目不适合公开,比如自己的私人项目或者自己的一些私人文件.
那么如何在自己的机器上或者云服务器上搭建一个自己的私人git服务器呢?
本文将介绍如何搭建一个自己的私人git服务器.

首先要有一个云服务器,或者自己的本地电脑安装好ubuntu系统.

## 服务器操作:

### 安装git和openssh

```
sudo apt-get install git
sudo apt-get install openssh
```

### 初始化仓库
```
cd ~
git init --bare about.git
```

### 生成.ssh目录
```
ssh-keygen
cd ~/.ssh
ls
```
可以看到如下目录结构
```
authorized_keys  id_rsa  id_rsa.pub
```

## 客户端操作:

### 生成key
```
ssh-keygen
cd ~/.ssh
ls
```
可以看到如下目录结构
```
authorized_keys  id_rsa  id_rsa.pub
```
然后执行:
```
cat ~/.ssh/id_rsa.pub
```
可以看到输出一段字符类似:
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC5LdkvYM4+NT3kTcr.......
```

## 服务器操作

```
cd ~
vim ~/.ssh/authorized_keys
```
将客户端上的这一段字符```ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC5LdkvYM4+NT3kTcr.......```拷贝到```authorized_keys```文件里,然后保存退出.

## 客户端操作:

### 克隆到本地
在客户端执行:
```
git clone 服务器用户名@ip:/about.git
```
可以看到输出如下字符(下面是我的操作的输出):
```
ruben@ruben:~$ git clone root@cpp.pub:about.git
Cloning into 'about'...
warning: You appear to have cloned an empty repository.
```

### 总结
到这里就完成了:

 - 1.在服务器建立git仓库
 - 2.在服务器添加客户端的pub key 
 - 3.拷贝远程仓库到本地

完成以上步骤就完成了本文的目标,下面就可以对代码或者文件进行版本管理啦~



