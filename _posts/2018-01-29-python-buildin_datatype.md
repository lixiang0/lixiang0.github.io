---
title: "python教程之3基本数据类型"
category: other
layout: post
tags: [python]
date: '2018-01-29 23:00:24'
---

上篇文章简单介绍了Python语言的基本语法，以及如何在IDE编写一个Python程序。

本文将介绍Python中的基本数据类型以及相关的操作。

### 基本数据类型

Python有五个标准的数据类型：

- Numbers（数字）
- String（字符串）
- List（列表）
- Tuple（元组）
- Dictionary（字典）

Python中创建变量时不需要声明具体的数据类型，由赋值时确定。比如：
```
i=1#整形
j=1.0#float型
k='qwer'#字符型
m=[1,2,3,4]#列表
n=(2,1,3)#元组
x={'mm':1}#字典型
```


#### 基本数据类型之数值型

数值型有下面几种类型：

- int（有符号整型）
- float（浮点型）
- complex（复数）

示例：
```
j=10#int
k=1.0#float
m=1+2j#complex,1为实部，2为虚部
n=complex(1,2)#complex,1为实部，2为虚部
```
注意：长整型也可以使用小写 l，但建议使用大写L，避免与数字1混淆。复数由实数部分和虚数部分构成，可以用 a + bj,或者 complex(a,b) 表示， 复数的实部 a 和虚部 b 都是浮点型。


#### 基本数据类型之字符串

字符串或串(String)是由数字、字母、下划线组成的一串字符。

一般记为 :
s="a1a2···an"(n>=0),表示文本的数据类型。

python的字串列表有2种取值顺序:
- 从左到右索引默认0开始的，最大范围是字符串长度少1
- 从右到左索引默认-1开始的，最大范围是字符串开头

如果要实现从字符串中获取一段子字符串的话，可以使用变量 [头下标:尾下标]，就可以截取相应的字符串，其中下标是从 0 开始算起，可以是正数或负数，下标可以为空表示取到头或尾。

比如：
```
str = 'Hello World!'
 
print str           # 输出完整字符串
print str[0]        # 输出字符串中的第一个字符
print str[2:5]      # 输出字符串中第三个至第五个之间的字符串
print str[2:]       # 输出从第三个字符开始的字符串
print str * 2       # 输出字符串两次
print str + "TEST"  # 输出连接的字符串
```

#### 基本数据类型之列表

列表支持字符，数字，字符串甚至可以包含列表（即嵌套）。

列表用 [ ] 标识，是 python 最通用的复合数据类型。

列表中值的切割也可以用到变量 [头下标:尾下标] ，就可以截取相应的列表，从左到右索引默认 0 开始，从右到左索引默认 -1 开始，下标可以为空表示取到头或尾。

加号 + 是列表连接运算符，星号 * 是重复操作。如下实例：
实例(Python 2.0+)

```
list = [ 'hello', 786 , 2.23, 'world', 70.2 ]
add = [123, 'python']
 
print list               # 输出完整列表
print list[0]            # 输出列表的第一个元素
print list[1:3]          # 输出第二个至第三个元素 
print list[2:]           # 输出从第三个开始至列表末尾的所有元素
print tinylist * 2       # 输出列表两次
print list + add    # 打印组合的列表
```
以上实例输出结果：
```
['hello', 786, 2.23, 'world', 70.2]
hello
[786, 2.23]
[2.23, 'world', 70.2]
[123, 'python', 123, 'python']
['hello', 786, 2.23, 'world', 70.2, 123, 'python']
```

#### 基本数据类型之元组

元组类似于List（列表）,用"()"标识。内部元素用逗号,且不能二次赋值，相当于只读列表。

```
tuple_list = ('hello', 786, 2.23, 'world', 70.2)
add_tuple = (123, 'python')
print(tuple_list)  # 输出完整元组
print(tuple_list[0] ) # 输出元组的第一个元素
print(tuple_list[1:3] ) # 输出第二个至第三个的元素
print(tuple_list[2:])  # 输出从第三个开始至列表末尾的所有元素
print(tuple_list * 2)  # 输出元组两次
print(tuple_list + add_tuple)  # 打印组合的元组
```
输出为：
```
hello
(786, 2.23)
(2.23, 'world', 70.2)
('hello', 786, 2.23, 'world', 70.2, 'hello', 786, 2.23, 'world', 70.2)
('hello', 786, 2.23, 'world', 70.2, 123, 'python')
```


#### 基本数据类型之字典

字典(dictionary)是除列表以外python之中最灵活的内置数据结构类型。

列表是有序的对象集合，字典是无序的对象集合。

两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。
字典用"{ }"标识。字典由索引(key)和它对应的值value组成。

```
dict = {}
dict['one'] = "This is one"
dict['two'] = "This is two"

namedict = {'name': 'ruben', 'code': 1, 'gender': 'man'}
```
输出如下：
```
{'one': 'This is one', 'two': 'This is two'}
{'name': 'ruben', 'code': 1, 'gender': 'man'}

```

### 数据类型之间的转换

Python提供了基本数据类型之间转换的内置方法：
|函|描述|
|-|-|
|int(x [,base])|将x转换为一个整数|
|long(x [,base] )|将x转换为一个长整数|
|float(x)|将x转换到一个浮点数|
|complex(real [,imag])|创建一个复数|
|str(x)|将对象 x 转换为字符串|
|repr(x)|将对象 x 转换为表达式字符串|
|eval(str)|用来计算在字符串中的有效Python表达式,并返回一个对象|
|tuple(s)|将序列 s 转换为一个元组|
|list(s)|将序列 s 转换为一个列表|
|set(s)|转换为可变集合|
|dict(d)|创建一个字典。d 必须是一个序列 (key,value)元组。|
|frozenset(s)|转换为不可变集合|
|chr(x)|将一个整数转换为一个字符|
|unichr(x)|将一个整数转换为Unicode字符|
|ord(x)|将一个字符转换为它的整数值|
|hex(x)|将一个整数转换为一个十六进制字符串|
|oct(x)|将一个整数转换为一个八进制字符串|
