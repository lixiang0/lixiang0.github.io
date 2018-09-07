---
title: "python中的class"
category: python
layout: post
tags: [python]
date: '2018-09-07 11:00:24'
---

之前的文章介绍了```module```和```package```。

我们知道```package```是以文件夹的形式组织的，每个文件夹下的```.py```文件称之为```module```。而```class```在每个```.py```文件中。

### 最基本的class

一个简单的```class```示例如下所示：

```
class MyClass:
    """A simple example class"""
    i = 12345#成员变量

    def f(self):#成员方法
        return 'hello world'
```

要实例化一个```class```可以通过```new instance=ClassName()```的方式实例化。而成员变量和成员方法可以通过```instance.name```或者```instance.function_name```的方式调用。

上述MyClass的示例如下：

```
c=MyClass()
print(c.i)
#12345
print(c.f())
#hello world
```

### 复杂一点的例子

更复杂一点的例子：

```
class Complex:
    i=[]
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i.append(imagpart)
```

调用方式：

```
x = Complex(3.0, -4.5)
print(x.r,x.i)
#3.0 [-4.5]
xx = Complex(3.0, -2)
print(xx.r,xx.i)
#3.0 [-4.5, -2]
```
这里添加了```__init__()```内置方法用于初始化```class```中的成员变量。这里可以看到类```Complex```的两个实例```x```和```xx```中成员变量```i```的输出是不同的。关于类中的变量作用域将在下文介绍，暂且不表。


### class中变量的作用域

首先让我们运行下面的代码：

```
def scope_test():
    def do_local():
        spam = "local spam"

    def do_nonlocal():
        nonlocal spam
        spam = "nonlocal spam"

    def do_global():
        global spam
        spam = "global spam"

    spam = "test spam"
    do_local()
    print("After local assignment:", spam)
    do_nonlocal()
    print("After nonlocal assignment:", spam)
    do_global()
    print("After global assignment:", spam)
spam='spam'
scope_test()
print("In global scope:", spam)
```

得到的输出是：

```
After local assignment: test spam
After nonlocal assignment: nonlocal spam
After global assignment: nonlocal spam
In global scope: global spam
```

下面将对上述代码进行分析：

首先定义了全局变量```spam```，并赋值‘spam’。

接着实例化类```scope_test()```，执行类中的代码：

```
    spam = "test spam"
    do_local()
    print("After local assignment:", spam)
    do_nonlocal()
    print("After nonlocal assignment:", spam)
    do_global()
    print("After global assignment:", spam)
```

 - 第一个变量spam的作用域是类```scope_test```，并将局部变量```spam```赋值为```test spam```。
 - ```do_local()```中```spam```变量的作用域是```do_local()```方法，因而只是创建了一个本地变量，并赋值为```local spam```，但在方法之外失效。
 - 此时，print方法打印的```spam```变量是第一步中的局部```spam```变量，输出即是```test spam```。
 - ```do_nonlocal()```方法中将```spam```变量通过```nonlocal```关键字表示使用的是局部变量，因而此时的spam是第一步声明的```spam```局部变量。此时```spam```变量的值变为```nonlocal spam```。
 - 按照上一步分系，此时打印的值应该是```nonlocal spam```
 - ```do_global()```中通过```global```关键字声明使用的```spam```是全局变量，因而全局变量spam的值修改为```global spam```
 - 这里输出的是局部变量spam，因而输出是```nonlocal spam```
 
最后回到最外层的代码：

```
print("In global scope:", spam)
```
这里的变量```spam```是全局变量，根据上面的分析可以知道```spam```已经被修改为```global spam```，因而输出是```global spam```。

以上介绍了```python```中```class```的基本使用方法，之后介绍了```class```中变量的作用域范围，了解之后基本就能掌握```class```的基本使用方法了。


