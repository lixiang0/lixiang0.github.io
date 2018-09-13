---
title: "python中的标准库（2）"
category: python
layout: post
tags: [python]
date: '2018-09-13 11:00:24'
---



### 格式化输出

- reprlib
```
import reprlib
reprlib.repr(set('supercalifragilisticexpialidocious'))
#"{'a', 'c', 'd', 'e', 'f', 'g', ...}"
```

- pprint

```
import pprint
t = [[[['black', 'cyan'], 'white', ['green', 'red']], [['magenta',
     'yellow'], 'blue']]]
pprint.pprint(t, width=30)
#[[[['black', 'cyan'],
#   'white',
#   ['green', 'red']],
#  [['magenta', 'yellow'],
#   'blue']]]
```

- textwrap

```
import textwrap
doc = """The wrap() method is just like fill() except that it returns
 a list of strings instead of one big string with newlines to separate
 the wrapped lines."""
print(textwrap.fill(doc, width=40))
#The wrap() method is just like fill()
#except that it returns a list of strings
#instead of one big string with newlines
#to separate the wrapped lines.
```
- locale

```
import locale
locale.setlocale(locale.LC_ALL, 'English_United States.1252')
'English_United States.1252'
conv = locale.localeconv()          # get a mapping of conventions
x = 1234567.8
locale.format("%d", x, grouping=True)
#'1,234,567'
locale.format_string("%s%.*f", (conv['currency_symbol'],
                      conv['frac_digits'], x), grouping=True)
#'$1,234,567.80'
```

### 多线程


```
import threading, zipfile
import time
class TestThread(threading.Thread):
    def __init__(self, instring):
        threading.Thread.__init__(self)
        self.out=instring

    def run(self):
        time.sleep(10)
        print(self.out)

background = TestThread('test string...')
background.start()
print('The main program continues to run in foreground.')
background.join()    # Wait for the background task to finish
print('Main program waited until background was done.')
```


### 日志输出

```
import logging
logging.debug('Debugging information')
logging.info('Informational message')
logging.warning('Warning:config file %s not found', 'server.conf')
logging.error('Error occurred')
logging.critical('Critical error -- shutting down')
```

### 列表操作

- bisect
```
import bisect
scores = ['a','aa','aaa','aaaaa','aaaaaaaaaa']
bisect.insort(scores, 'aaaa')
print(scores)
#['a', 'aa', 'aaa', 'aaaa', 'aaaaa', 'aaaaaaaaaa']
```

- deque
```
from collections import deque
d = deque(["task1", "task2", "task3"])
d.append("task4")
print("Handling", d.popleft(),d.pop())
#Handling task1 task4
```

- array
```
from array import array
a = array('H', [4000, 10, 700, 22222])
print(sum(a))
print(a[1:3])
#26932
array('H', [10, 700])
```

- heapq
```
from heapq import heapify, heappop, heappush
data = [1, 3, 5, 7, 9, 2, 4, 6, 8, 0]
heapify(data)                      # rearrange the list into heap order
heappush(data, -5)                 # add a new entry
[heappop(data) for i in range(3)]  # fetch the three smallest entries
#[-5, 0, 1]
```

### 浮点数

- decimal
```
from decimal import *
round(Decimal('0.70') * Decimal('1.05'), 2)
#Decimal('0.74')
round(.70 * 1.05, 2)
#0.73
```
