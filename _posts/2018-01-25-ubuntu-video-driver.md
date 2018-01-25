---
title: "Ubuntu命令行安装nvidia显卡驱动"
category: other
layout: post
tags: [other,ubuntu]
date: '2018-01-25 21:30:24'
---


执行下面的命令：
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt-get install nvidia-384
```

使用```nvidia-smi```查看GPU的状态。
比如本文使用的GPU：
```
Thu Jan 25 21:40:28 2018
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 387.34                 Driver Version: 387.34                    |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 108...  Off  | 00000000:02:00.0 Off |                  N/A |
| 23%   40C    P0    54W / 250W |      0MiB / 11171MiB |      1%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

