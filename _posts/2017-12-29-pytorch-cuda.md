---
title: "[Pytorch]1.Training on GPU"
catagories: Pytorch
layout: post
date: '2017-12-29 18:00:24'
---

```
import torch
import torch.nn as nn
import torch.autograd as autograd
import torch.optim as optim

#how to validate cuda available
if torch.cuda.is_available():
    print('cuda is on')
else:
    print('cuda is off')

#if available
#allocate tensor to default device
x=torch.LongTensor(1)
if torch.cuda.is_available():
    x.cuda()
if torch.is_tensor(x):
    print('x is a tensor')
print(torch.cuda.device_count())
#transfer tensor to a specified device
y=torch.LongTensor(1).cuda(0)
#you can use tensor.get_device() to show which device tensor located
print(y.get_device())
#gernerally,specified context manager to run code
with torch.cuda.device(0):
    x=torch.cuda.LongTensor(1)
    x=torch.randn(1,2).cuda(0)#even in context you can specified a device to locate tensor


#device-agnostic code
isCuda=torch.cuda.is_available()
x=torch.Tensor(1,2)
if isCuda:
    x=x.cuda()
print(torch.eye(3,4))
```