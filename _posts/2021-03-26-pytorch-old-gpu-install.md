---
title: "在老旧GPU上安装pytorch的方法"
category: dl
layout: post
tags: [Pytorch,dl]
date: '2021-03-26 17:42:24'
---


本着节约的原则花1000块买了一块k40c的显卡，但是在运行pytorch直接就出现了这个问题：
```
RuntimeError: CUDA error: no kernel image is available for execution on the device
Turns out that PyTorch v1.6.0 dropped support for GPUs with NVIDIA compute capability 3.5 in their prebuilt binaries that you'd get from pip or conda —the stated reason was that supporting these older GPUs would have pushed binary sizes past acceptable limits for distribution.
```

看来只能试着源码安装。无奈源码安装也遇到了各种问题。于是谷歌一番找到了适合老旧GPU的pytorch安装包。

由于使用pip安装比较简单，这里就直接列出来：

- 仓库地址：https://github.com/nelson-liu/pytorch-manylinux-binaries/releases

- 安装示例：
    ```
    pip install torch==1.8.0+cu111 -f https://nelsonliu.me/files/pytorch/whl/torch_stable.html
    ```
打开链接'''https://cs.stanford.edu/~nfliu/files/pytorch/whl/torch_stable.html'''可以看到各种版本pytorch+cuda的安装包（比如1.8.0）：
```
torch-1.8.0+cu101-cp36-cp36m-linux_x86_64.whl
torch-1.8.0+cu101-cp37-cp37m-linux_x86_64.whl
torch-1.8.0+cu101-cp38-cp38-linux_x86_64.whl
torch-1.8.0+cu101-cp39-cp39-linux_x86_64.whl
torch-1.8.0+cu102-cp36-cp36m-linux_x86_64.whl
torch-1.8.0+cu102-cp37-cp37m-linux_x86_64.whl
torch-1.8.0+cu102-cp38-cp38-linux_x86_64.whl
torch-1.8.0+cu102-cp39-cp39-linux_x86_64.whl
torch-1.8.0+cu111-cp36-cp36m-linux_x86_64.whl
torch-1.8.0+cu111-cp37-cp37m-linux_x86_64.whl
torch-1.8.0+cu111-cp38-cp38-linux_x86_64.whl
torch-1.8.0+cu111-cp39-cp39-linux_x86_64.whl
```