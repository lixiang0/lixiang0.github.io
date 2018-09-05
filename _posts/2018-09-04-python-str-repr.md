---
title: "python中str和repr"
category: other
layout: post
tags: [python]
date: '2018-09-04 00:00:24'
---

python3中格式化输出经常用到的方法，一种是```str()```，一种是```repr()```。

### 1.f''作为格式化输出

在字符串前添加f，变量使用```{变量名}```格式输出。```：```表示字符串的宽度。
```
a='abcdefg'
print(f'{a}')
print(f'{a:10}1')
```
另外在python2中常使用的```format```在python3中依然有效：
```
#format
print('{},{}'.format(a,b))
print('{1},{0}'.format(a,b))#定义输出顺序
```

### 2.str()方法

```str```方法用于将其他类型的变量转换为字符串。

```
#str
a=1234.123456
print(str(a))
print(f'{a:.5f}')#表示精度
print(f'{a:.5}')#表示宽度
print(str(a).center(14))#表示数字居中，宽度为14
```

### 2.repr()方法

```repr```方法是完整的输出字符串，比如```a='a'```,那么```repr(a)```输出的是字符串对象```'a'```。

```
#repr
a='a';b='ss'
print(repr(a),repr(b))
print(repr(a).rjust(4),repr(b).ljust(4))#宽度4,右对齐和左对齐
#!s !r !a
print(f'{a !a}')#asicii形式输出
print(f'{a !r}')#repr字符串对象形式输出
print(f'{a !s}')#str字符串输出

table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; '
      'Dcab: {0[Dcab]:d}'.format(table))
```

### 3.str和repr作为对象的内置方法

```
class Out():
	def __init__(self,x,y):
		self.x=x
		self.y=y
	def __str__(self):
		return self.x+'  '+self.y
	def __repr__(self):
		return repr(self.x)+repr(self.y)
o=Out('sss','zzz')
print(o)
print(repr(o))
```
