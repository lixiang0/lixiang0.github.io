---
title: "python教程之1环境配置和IDE"
category: other
layout: post
tags: [other,python]
date: '2018-01-26 00:00:24'
---

入坑Python差不多一年了，一直想把学习经历写下来，但是总是因为懒而迟迟没有开始。

本文作为第一篇作为入门篇，首先将介绍粗略的介绍下python，然后介绍如何将python在Windows中的环境搭建起来(笔者比较喜欢用Ubuntu和sublime)。

## 初识Python

相信很多的读者已经了解过Python这门语言，或者已经在这做过一些尝试了。近年来Python越来越火爆，究其原因，笔者认为最大的特点是适合偷懒吧。因为Python 是一个高层次的结合了解释性、互动性和面向对象的脚本语言。


### 解释性
为什么说它高层次呢？举个例子，你的领导说：哎，小刘啊，你过来，我们的APP新增一个功能，大概就是要这样这样，懂了吗？你去实现吧。至于怎么实现领导就完全不管了。

在Python中，你也可以成这样的领导。举个栗子：

![](/imgs/python-1-1.png)


比如说需要下载一个网页，在java中会怎么做呢？
java中需要依次完成下面的操作：

- 构造一个URL对象
- 打开连接
- 构造连接属性
- 建立连接
- 获取响应头
- 构造输入流
- 从输入流中读取数据
- 解码

java中需要正确的完成以上步骤才能下载一个网页。

而在Python只需要下面几行代码：

```
import requests
response = requests.get(url)
print(response.content)
```
引入网络模块，给get方法传入url参数，获取网页内容。完毕！

是不是很简单呢？Python是不是让事情简单了很多。


### 可读性

Python的代码看起来就像是人类语言，最大的区别就是没有```{}```。python中是使用空格来对齐的，至于空格的个数没有限制，习惯上通过```tab```来进行缩进。
比如：
```
'我是注释'
for i in range(5):
    for j in range(6):
        print(str(i*j))
```
上述代码通过使用一个```tab```的缩进来使代码分块（Java、cpp等是使用```{}```），并且代码块之间通过```:```来表示开始新的代码块。

### 互动性

Python 是交互式语言，设置可以通过命令行来写代码。

![](/imgs/python-1-7.png)

像图中显示的那种。Python可以直接当做计算器来用，一行输入对应一个输出。
### 面向对象

Python 是面向对象语言，这点这里不做过多的解释了~


## 下载Python

### 安装
打开Python的官网下载界面：https://www.python.org/downloads/。

![](/imgs/python-1-2.png)

选择python 3.6.4版本，单击既可下载了。

如果你懒得话，这里直接给出了[链接](https://www.python.org/ftp/python/3.6.4/python-3.6.4.exe
)。

下载完毕之后，双击打开如下图所示：
![](/imgs/python-1-3.png)

选择```install now```就好了(也可以自定义，比如选择其他的安装路径)。然后就看到这样的界面：

![](/imgs/python-1-4.png)

完成安装之后点击```close```.

### 配置环境变量
安装好了之后，按照下面的步骤设置环境变量

![](/imgs/python-1-5.png)

- 右键点击"计算机"，然后点击"属性"
- 然后点击"高级系统设置"
- 选择"系统变量"窗口下面的"Path",双击即可！
- 在"Path"行最前面添加python安装路径即可（默认为C:\Users\Administrator\AppData\Local\Programs\Python\Python36-32）。记住，路径直接用英文分号";"隔开。也就是将```C:\Users\Administrator\AppData\Local\Programs\Python\Python36-32;```复制到最前面（如果不是使用默认路径为```你的安装路径;```）。
- 设置成功以后，在cmd命令行，输入命令"python"，就可以有相关显示。
- 
![](/imgs/python-1-6.png)

## 下载IDE

本文介绍的IDE是[pycharm](https://www.jetbrains.com/pycharm/download/),打开官网链接之后选择社区版本（或者如果你懒得打开官网，直接右键[下载链接](https://download.jetbrains.8686c.com/python/pycharm-community-2017.3.3.exe)另存为）。

![](/imgs/python-1-8.png)


下载之后双击，下一步完成安装。

选择```Do not import settings```

![](/imgs/python-1-9.png)

选择```accept```:

![](/imgs/python-1-10.png)

选择IDE的主题，本文选择的是```Darcula```:

![](/imgs/python-1-11.png)

选择```Create New Project```:

![](/imgs/python-1-12.png)

然后就是选择项目的保存地址和python的路径了。参照下图配置。

![](/imgs/python-1-13.png)

然后点击```Create```，就进入主界面了，是不是跟```Android Studio```很像呢？

## 熟悉IDE

首先下载项目代码：
```
git clone git@github.com:lixiang0/baike-spider.git

```
或者右键[另存为](https://codeload.github.com/lixiang0/baike-spider/zip/master)。下载之后解压。

在IDE界面选择```File->open```打开刚才解压的目录。

![](/imgs/python-1-14.png)


双击```spider_main.py```，复制如下代码：

```
print('hello world!')
```

右键```spider_main.py```选择```Run spider_main```,如下图所示：

![](/imgs/python-1-16.png)

好了~

第一个Python程序就完成了~

下一篇文章继续吧。


