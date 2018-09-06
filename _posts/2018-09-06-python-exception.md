---
title: "python中的exception"
category: python
layout: post
tags: [python]
date: '2018-09-06 00:00:24'
---

### Exception

在python中运行如下代码将会报错：
```
while True print('Hello world')
  File "<stdin>", line 1
    while True print('Hello world')
                   ^
SyntaxError: invalid syntax
```
而正确的代码应该是:
```
while True:
    print('Hello world')
        while True:
            print('Hello world')
```

这是因为python解释器会对程序的错误抛出异常。类似的错误还有：
```
>>> 10 * (1/0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero


>>> 4 + spam*3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'spam' is not defined


>>> '2' + 2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't convert 'int' object to str implicitly
```
### 处理Exception

像其他语言一样，我们可以使用```try...except...```关键字对这些异常进行捕获并进行处理：

```
while True:
    try:
        x = int(input("Please enter a number: "))
        break
    except ValueError:
        print("Oops!  That was no valid number.  Try again...")
```

或者一次性处理多个异常，并忽略：
```
while True:
    try:
        x = int(input("Please enter a number: "))
        break
    except (RuntimeError, TypeError, NameError):
        pass
```
### 自定义Exception

我们可以自己定义一个异常，这样针对自定义的错误抛出异常。
```
>>> raise NameError('HiThere')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: HiThere
```

还可以自定义一个异常类：
```
class InputError(Error):
    """针对输入异常的自定义异常类

    Attributes:
        expression -- 哪一段代码异常
        message -- 异常的说明
    """

    def __init__(self, expression, message):
        self.expression = expression
        self.message = message
```


自定义异常之后，在编写代码的过程中可以自定义异常，比如：
```
raise InputError
```


### 对Exception处理后的终极操作
```
    try:
        raise KeyboardInterrupt
    finally:
        print('Goodbye, world!')
```
```finally```是对异常处理之后的清扫工作，指的是处理完异常之后还要进行的操作，比如上报异常、记录异常、日志等工作。
