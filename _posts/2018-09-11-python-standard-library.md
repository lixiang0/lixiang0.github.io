---
title: "python中的标准库（1）"
category: python
layout: post
tags: [python]
date: '2018-09-11 11:00:24'
---




- os库

```
import os
os.getcwd()#返回当前的工作目录
#'/home/ruben'
os.chdir('/server/accesslogs')   #改变当前工作目录
os.system('mkdir today')   #新建目录
dir(os)
#['CLD_CONTINUED', 'CLD_DUMPED', 'CLD_EXITED', 'CLD_TRAPPED', 'DirEntry', 'EX_CANTCREAT', 'EX_CONFIG', 'EX_DATAERR', 'EX_IOERR',.......返回os的内置方法、内置变量等
help(os)
#返回os包的帮助信息:
```
os库包含的是许多关于操作系统的相关操作

- shutil库

```
import shutil
shutil.copyfile('data.db', 'archive.db')#拷贝文件
shutil.move('/build/executables', 'installdir')#移动文件
```
shutils是关于文件相关的操作

- glob

```
import glob
glob.glob('*.py')#枚举文件
#['primes.py', 'random.py', 'quote.py']
```
glob是关于文件或文件夹的列举操作

- sys

```
import sys
print(sys.argv)
#['demo.py', 'one', 'two', 'three']
sys.stderr.write('Warning, log file not found starting a new one\n')#命令行输出错误信息
sys.exit()#退出脚本
```
sys是关于命令行中参数的获取，比如```python demo.py one two three```。获取到的第一个参数是代码文件名，第二到第四个参数是用于输入的自定义参数。

- re
- 
正则操作
```
import re
re.findall(r'\bf[a-z]*', 'which foot or hand fell fastest')
#['foot', 'fell', 'fastest']
re.sub(r'(\b[a-z]+) \1', r'\1', 'cat in the the hat')
#'cat in the hat'
'tea for too'.replace('too', 'two')
#'tea for two'
```

- math


数学操作
```
import math
math.cos(math.pi / 4)
#0.70710678118654757
math.log(1024, 2)
#10.0
```
- random

随机数的产生
```
import random
random.choice(['apple', 'pear', 'banana'])
#'apple'
random.sample(range(100), 10)   # sampling without replacement
#[30, 83, 16, 4, 8, 81, 41, 50, 18, 33]
random.random()    # random float
#0.17970987693706186
random.randrange(6)    # random integer chosen from range(6)
#4
```

- statistics


统计相关操作
```
import statistics
data = [2.75, 1.75, 1.25, 0.25, 0.5, 1.25, 3.5]
statistics.mean(data)
#1.6071428571428572
statistics.median(data)
#1.25
statistics.variance(data)
#1.3720238095238095
```

- urllib

网络访问
```
from urllib.request import urlopen
with urlopen('http://tycho.usno.navy.mil/cgi-bin/timer.pl') as response:
     for line in response:
         line = line.decode('utf-8')  # Decoding the binary data to text.
         if 'EST' in line or 'EDT' in line:  # look for Eastern Time
             print(line)
#<BR>Nov. 25, 09:43:32 PM EST
```

- smtplib

```
import smtplib
server = smtplib.SMTP('localhost')
server.sendmail('soothsayer@example.org', 'jcaesar@example.org',
"""
To: jcaesar@example.org
From: soothsayer@example.org
Beware the Ides of March.
""")
server.quit()
```

- datetime

时间相关操作
```
from datetime import date
now = date.today()
now.strftime("%m-%d-%y. %d %b %Y is a %A on the %d day of %B.")
#'09-11-18. 11 Sep 2018 is a Tuesday on the 11 day of September.'
datetime.date(2018, 11, 9)
birthday = date(1964, 7, 31)
age = now - birthday
age.days
#14368
```


- zlib,gzip, bz2, lzma, zipfile,tarfile.

文件或字符压缩
```
import zlib
s = b'witch which has which witches wrist watch'
len(s)
#41
t = zlib.compress(s)
len(t)
#37
zlib.decompress(t)
#b'witch which has which witches wrist watch'
zlib.crc32(s)
#226805979
```

- timeit

性能测试
```
from timeit import Timer
Timer('t=a; a=b; b=t', 'a=1; b=2').timeit()
#0.57535828626024577
Timer('a,b = b,a', 'a=1; b=2').timeit()
#0.54962537085770791
```

- doctest

文档测试
```
def average(values):
    """Computes the arithmetic mean of a list of numbers.

    >>> print(average([20, 30, 70]))
    40.0
    """
    return sum(values) / len(values)

import doctest
doctest.testmod()   
```
- unittest

单元测试
```
import unittest
class TestStatisticalFunctions(unittest.TestCase):

    def test_average(self):
        self.assertEqual(average([20, 30, 70]), 40.0)
        self.assertEqual(round(average([1, 5, 7]), 1), 4.3)
        with self.assertRaises(ZeroDivisionError):
            average([])
        with self.assertRaises(TypeError):
            average(20, 30, 70)

unittest.main() 
```

上面介绍的是一些基本的标准库，还有提供rpc服务的xmlrpc，邮件服务的email，json解析的json库，sqlite数据库的sqlite3...等等，这些标准库完成了许多标准化操作。另外还有更多的第三方库这里就不一一列举了。
