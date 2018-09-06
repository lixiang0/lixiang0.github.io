---
title: "python中module和package"
category: python
layout: post
tags: [python]
date: '2018-09-05 00:00:24'
---

python中的```module```和```package```分别以文件和文件夹形式组织的。

### module定义

module的基本形式为：

```
# Fibonacci numbers module

def fib(n):    # write Fibonacci series up to n
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()
```

文件命名为：```fib.py```，这样一个文件为一个module。
 
 
### module引用

对modul的引用方式为：```import fib```，即```import filename```。引用之后对module其中的方法调用方式为：```fib.fib```。即```filename.functionname```。
 
 
或者更为简洁的可以直接引用某个方法：```form fib import fib```或者```from fib import *```表示引入所有的方法。此时对module中某个方法的调用方式为：```fib```即可。
 
如果要查看某个module下有哪些方法可以通过：
 ```
 import sys
 dir(fib)
 ```
的方式查看module的中所有方法。
 
值得注意的是：
 
不管是```import module 或者 方法```都可以使用```as```关键字进行重命名。
比如```import fib as f```或者```import fib.fib as f```。
 
 
### package
 
package是以文件夹的形式划分的，每一个package里面还包含多个文件（即module）。

package的组织形式为：
 ```
 path1/path2/fib.py
 ```
此时对fib的引用方式为：
 ```
 import path1.path2.fib
 ```
 
 
### import的查找路径
 
python解释器会先查找环境变量中可能路径，然后在搜索自定义路径中的module文件。
 
如果需要添加自定义路径，通过：
 ```
import sys
sys.path.append('/user/custom/lib/python')
```
的方式添加自定义路径。
