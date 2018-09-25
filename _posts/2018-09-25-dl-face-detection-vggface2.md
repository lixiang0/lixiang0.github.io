---
title: "人脸识别之VGGFace2"
category: dl
layout: post
tags: [dl]
date: '2018-09-25 11:00:24'
---


VGGFace2是一个大规模人脸识别数据集。数据的来源是谷歌搜索引擎.数据标注了姿态、年龄、光照、种族和职业。

### 数据的特色


<img src='http://www.robots.ox.ac.uk/~vgg/data/vgg_face2/img/gender2.png' width=200></img>

- 9,000+特性，包含年龄、种族、职业等


<img src='http://www.robots.ox.ac.uk/~vgg/data/vgg_face2/img/train_val2.png' width=200></img>

- 33亿张人脸：所有人脸都是在自然条件下的，并且经过了姿态、情绪验证，分别有不同光照、遮挡条件。


<img src='http://www.robots.ox.ac.uk/~vgg/data/vgg_face2/img/facesize.png' width=200></img>

- 每个类别平均有362张图片，图片在每个类别下的分布均匀，少的有87,多的有862张。

### 数据和模型下载链接

- [人脸数据](http://www.robots.ox.ac.uk/~vgg/data/vgg_face2/data_infor.html)

- [人脸属性信息](http://www.robots.ox.ac.uk/~vgg/data/vgg_face2/meta_infor.html)

- [模型下载链接](https://github.com/ox-vgg/vgg_face2)：训练集：VGGFace2测试集：IJB

### 论文
Q. Cao, L. Shen, W. Xie, O. M. Parkhi, A. Zisserman  
[VGGFace2: A dataset for recognising face across pose and age](http://www.robots.ox.ac.uk/~vgg/publications/2018/Cao18/cao18.pdf)  
International Conference on Automatic Face and Gesture Recognition, 2018.
