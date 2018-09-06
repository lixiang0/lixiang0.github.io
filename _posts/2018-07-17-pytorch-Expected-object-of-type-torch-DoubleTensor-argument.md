---
title: "RuntimeError: Expected object of type torch.DoubleTensor but found type torch.FloatTensor for argument #2 'weight'解决办法"
category: dl
layout: post
tags: [Pytorch,dl]
date: '2018-07-17 17:42:24'
---



```
RuntimeError: Expected object of type torch.DoubleTensor but found type torch.FloatTensor for argument #2 'weight'
```
今天遇到这个问题，一开始以为是输入的Tensor的问题，后来一检查发现是Model中的weight的数据类型跟输入不同的关系。

输入的是DoubleTensor类型，而模型默认的是FloatTensor类型，导致数据类型不一致报错。

解决的办法就是在模型创建和输入的时候统一数据类型，比如：
```
		self.cnn7=torch.nn.Conv2d(1, 1, (7,100), stride=(1,1),padding=(3,0)).float()
		self.linear=torch.nn.Linear(3,2).float()
```

另外值得注意的一点是FloatTensor在CPU中的执行效率比DoubleTensor更高。因为尽量采用FloatTensor类型。
