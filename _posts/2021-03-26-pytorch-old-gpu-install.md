---
title: "在老旧GPU上安装pytorch的方法"
category: dl
layout: post
tags: [Pytorch,dl]
date: '2021-03-26 17:42:24'
---


## 20210526更新
从结果来看，本文的方法依然不能投太多的懒，所以后来笔者就亲自编译了torch 1.9和torchvision 0.9的whl安装文件。
这里详细的编译过程就不赘述，直接列出安装文件，需要的读者可以直接下载安装使用。
注意的是在执行pip操作之前需要安装最新的cuda和cudnn以及最新的驱动,参考博文[Ubuntu16.04下如何安装显卡驱动、cuda、cudnn](https://blog.youran.ai/posts/ubuntu-cuda-cudnn-driver.html)。
以笔者的为例：
- 系统版本是ubuntu 16.04 LTS
- 显卡有2块：1块1660TI，1块M40 24G
- 驱动465，cuda版本11.3，cudnn 8.2
```
Wed May 26 17:04:49 2021       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 465.19.01    Driver Version: 465.19.01    CUDA Version: 11.3     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:01:00.0 Off |                  N/A |
|  0%   38C    P8     9W / 140W |    198MiB /  5942MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA Tesla M4...  Off  | 00000000:05:00.0 Off |                    0 |
| N/A   29C    P8    19W / 250W |      1MiB / 22945MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1217      G   /usr/lib/xorg/Xorg                146MiB |
|    0   N/A  N/A      1908      G   compiz                             49MiB |
+-----------------------------------------------------------------------------+
```
pytorch 1.9和torchvision 0.9的安装包链接如下：
```
链接：https://pan.baidu.com/s/19gDdmkTeL9ThnQ5s2rHcig 
提取码：b7me 
复制这段内容后打开百度网盘手机App，操作更方便哦
```

## 以下是原文
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
