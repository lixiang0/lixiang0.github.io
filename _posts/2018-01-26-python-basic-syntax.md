---
title: "python教程之2基本语法"
category: python
layout: post
tags: [python]
date: '2018-01-26 23:00:24'
---

上篇文章简单介绍了Python语言以及IDE的搭建。

本文将介绍Python的基本语法，以及如何在IDE编写Python程序。

## 创建和运行第一个项目
首先打开IDE，然后选择```File->New Project```,之后按照下面设置：

![](/imgs/python-2-1.png)

点击```Create```，选择```open in new window```。就创建好了新的项目了。如下所示：

![](/imgs/python-2-2.png)

对着项目名右键，选择```New->Python File```,在弹出的输入框输入文件名，比如：

![](/imgs/python-2-3.png)

然后点击```ok```。双击```1.hello_world.py```文件，如下图所示：

![](/imgs/python-2-4.png)

复制如下代码，然后右键```1.hello_world.py```文件，选择```Run 1.hello_world```可以看到输出：
```
word = 'word'
sentence = "这是一个句子。"
paragraph = """这是一个段落。
包含了多个语句"""


# 文件名：1.hello_world.py

# 第一个注释
is_new=True
if is_new:
    print("Hello, World!") # 第二个注释
else:
    print("I know Python!")  # 第三个注释
```
![](/imgs/python-2-5.png)

到这为止就创建和运行了我们的第一个Python项目和第一个Python程序了。下面将介绍Python的基本语法，这些基本的语法是需要牢记的。


## 基本语法

### 命名规则

在编写实际的代码之前将首先介绍一下Python的基本语法，然后再进行实际的编程。

- 在 Python里，变量或者保留字段是由字母、数字、下划线组成并区分大小写，开头可以是英文、数字或者下划线(_)，但有一点不能以数字开头。

- 以下划线开头的标识符是有特殊意义的。以单下划线开头 _name 的代表不能直接访问的类属性，需通过类提供的接口进行访问，不能用 from xxx import * 而导入

- 以双下划线开头的```__name```代表类的私有成员；以双下划线开头和结尾的```__name__```代表Python 里特殊方法专用的标识，如``` __init__()```代表类的构造函数。

- Python 可以同一行显示多条语句，方法是用分号 ; 分开，如：
```print('code1');print('code2'));```

### 保留字段

和其他编程语言一样，Python也有自己的保留字段。保留字段不能用来定义变量并赋值。
Python中保留字段如下：

||||
|-|-|-|
|and|exec|not|
|assert|	finally|	or|
|break|	for|	pass|
|class|	from|	print|
|continue|	global|	raise|
|def|	if|	return|
|del|	import|	try|
|elif|	in	|while|
|else|	is|	with|
|except|	lambda|	yield|

### 输出
Python中使用```print```输出，默认输出是换行的，如果要实现不换行需要在变量末尾加上逗号```,```。比如：
```
print('1')
print('1','2')
```

### 代码分块和缩进

在其他语言中，代码分块是通过```{}```来实现的，而Python中是通过代码的缩进以及```:```来实现的。
比如：
```
if True:
    print("True")
else:
    print("False")
```
这段代码相当于Java中的：
```
if(1){
    System.out.print('True');
    }else{
    System.out.print('False');    
    }
```
代码的分块是由```tab```键区分（也可以是任意数量的空格）进行的，可以把```{}```理解成用空格代替了。

在编写代码的过程中，如果没有统一的空格进行缩进，那么就会报```IndentationError: unexpected indent```错误。当看到这个错误时，就需要检查自己代码中缩进时候统一了。

下面是一个代码缩进的错误例子：
```
print('1')
    print('2')
print('3')

```
正确的应该是：
```
print('1')
print('2')
print('3')
```
### 多行语句
Python语句中一般以新行作为为语句的结束符。
但是我们可以使用斜杠（ \）将一行的语句分为多行显示，如下所示：
```
total = item_one + \
        item_two + \
        item_three
```

### 引号
Python 可以使用引号( ' )、双引号( " )、三引号( ''' 或 """ ) 来表示字符串，引号的开始与结束必须的相同类型的。
其中三引号可以由多行组成，编写多行文本的快捷语法，常用于文档字符串，在文件的特定地点，被当做注释。
```
word = 'word'
sentence = "这是一个句子。"
paragraph = """这是一个段落。
包含了多个语句"""
```

### 注释
python中单行注释采用 ```#``` 开头。
```
# 文件名：1.hello_world.py

# 第一个注释
print("Hello, World!") # 第二个注释
```
输出结果：
```
Hello, World!
```
好了~
本文介绍了Python的基本语法，并编写和运行第一个Python程序。

下文将介绍Python的基本数据类型。
