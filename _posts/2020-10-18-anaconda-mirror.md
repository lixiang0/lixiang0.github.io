---
title: "如何创建自己的私有conda镜像"
category: other
layout: post
tags: [conda,python]
date: '2020-10-18 16:00:24'
---
本文的组成：

第一部分解释创建自己的镜像的动机;

第二部分介绍分析的过程

第三部分直接贴出具体的步骤。



一、动机



    anaconda提供方便的软件包管理方式，通过它能够很方便的使用众多的开源包。但anaconda对国内用户是相当的不友好，下载速度超级慢；之前国内有众多的镜像源解决了这个问题，但去年的第三方源关闭的风波直接导致国内没有一个国内源能供使用。因而如何创建自己的私人镜像就显得很重要了，这将在我们实际的开发过程中节省大量的下载时间。

![](imgs/conda1.png)

<center>图1 anaconda官网的介绍</center>

二、分析



2.1 总体思路



    由于python为开源语言，python的安装包一般就是源码的打包，因而下载的安装文件也就是python源码的压缩包，所以创建镜像的思路就是：自动的将软件库中各种包下载到本地，然后设置本地源为本地路径即可。



2.2 分析源的结构   



    anaconda源分为商业版和官方版两种，两种源如下：

![](imgs/conda-mirror2.png)


<center>图2 社区版</center>

![](imgs/conda-mirror3.png)

<center>图3 官方版</center>

图2、图3就是仓库的首页了，打开```https://repo.anaconda.com/pkgs/main/linux-64/```可以看到linux-64平台下的所有的包：

![](imgs/conda-mirror4.png)

<center>图4 linux-64下的所有包</center>

从上面的分析可以看出，

社区版本的包网络路径为:
```
https://conda.anaconda.org/{channel}/{platform}/{file_name}
```
官方版本为：
```
https://repo.anaconda.org/{channel}/{platform}/{file_name}
```
这样就确定了包的下载路径了。



到这里，就确定了具体的镜像思路了：只需要抓取对应源下的平台下的所有包，即可完成镜像。



2.3 设置本地源



由包的链接可以得出抓取之后的路径为：
```
└── anaconda
    ├── cloud
    │   └── conda-forge
    │       ├── linux-64
    │       └── noarch
    └── pkgs
        ├── free
        │   ├── linux-64
        │   └── noarch
        ├── main
        │   ├── linux-64
        │   └── noarch
        └── pro
            ├── linux-64
            └── noarch
```
在抓取之后，需要将本地conda环境设置为本地源：
```
conda config --set channel_alias file://Path_to_your_channel/anaconda/pkgs
conda config --add channels free
conda config --add channels pro
conda config --add channels main
conda config --add channels conda-forge
conda config --remove channels defaults
conda config --set offline True
```

然后修改```~/.condarc``` :
```
channels:
  - conda-forge
  - main
  - pro
  - free
channel_alias: file://Path_to_your_channel/anaconda/pkgs
```
之后通过config --get命令查看具体的设置 :
```
conda config --get
--set channel_alias file://Path_to_your_channel/anaconda/pkgs
--add channels 'free'   # lowest priority
--add channels 'pro'
--add channels 'main'
--add channels 'conda-forge'   # highest priority
--set offline True
```
之后想要移除可以通过下面的命令来移除：

```conda config --remove channels <your_mistake>```

以上，即完成了对官方源和社区源的镜像。



2.4 部分改进



  本项目参考了开源项目conda-mirror，并在之上进行了部分改进和优化：

- 1.添加下载进度条；

- 2.添加多线程下载；

- 3.添加main、free的channel支持；

- 4.取消缓存目录在部分操作删除已下载包



三、使用步骤



3.1 安装
```
git clone https://github.com/lixiang0/conda-mirror
cd conda-mirror
python setup.py install
```

3.2 使用示例



下载目录下创建conf.yaml，内容为：
```
blacklist:
    - build: 'py2*'
whitelist:
    - build: 'py3*'
```
释义：屏蔽python2的版本，只下载python3的版本包



执行命令：
```
conda-mirror --upstream-channel main  --platform linux-64 -vvv --num-threads 12 --temp-directory ./temp/ -k --config conf.yaml
```

释义：

- platform：下载对应平台下的包

- vvv:显示warnning信息

- num-threads下载和验证线程数目

- temp-directory：缓存目录

- k：不使用https

- config：包过滤配置

运行截图：

![](imgs/conda-mirror1.png)

更多的详细修改，可以参考github：```https://github.com/lixiang0/conda-mirror```



参考链接：
```

1.https://www.anaconda.com/products/individual

2.https://conda-forge.org/feedstocks/

3.https://repo.anaconda.com/pkgs/

4.https://dreambooker.site/2018/11/16/Set-up-personal-Anaconda-mirror/

5.https://pypi.org/project/conda-mirror/

6.https://docs.python.org/3/library/multiprocessing.html#multiprocessing.pool.Pool

7.https://github.com/Valassis-Digital-Media/conda-mirror
```