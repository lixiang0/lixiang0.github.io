---
title: "[Tensorflow]1.Installing TensorFlow on Ubuntu"
catagories: ml
layout: post
date: '2017-08-17 00:33:24'
---

3tensorflow的官方安装文档参考：[链接](https://www.tensorflow.org/install/install_linux#InstallingVirtualenv)，注意：需要梯子

---
tensorflow有三种安装方式，分别为：

-  virtualenv
- "native" pip
- Docker
- Anaconda

本文是在Ubuntu 14.04 64bit desktop版本下使用virtualenv的方式安装。注意python版本使用的3.4版本。
执行：
```
sudo apt-get install python3-pip python3-dev python-virtualenv 
virtualenv --system-site-packages ～/tf_ws
cd ~/tf_ws
source bin/activate
```
到这，就进入了虚拟环境了。接下来执行：
```
pip install --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.2.1-cp34-cp34m-linux_x86_64.whl
```
执行完毕就完成了tensorflow的安装了。

下面验证是否安装成功。
执行：
```
python3
import tensorflow as tf
node=tf.constant("1")
print(node)
```
可以看到如下输出：
```
Tensor("Const:0", shape=(), dtype=int32)
```
表示安装成功～