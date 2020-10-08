---
title: ""
category: python
layout: post
tags: [python]
date: '2020-10-08 16:00:24'
---
### 1.引言

之前写过如何编写一个微博爬虫的文章，后来将微博爬虫开源到了GitHub上。
传统的视频图片的抓取姿势是如何的呢？如果使用requests包可以简单到下面这样的一句代码：

```
requests.get(img_url,stream=True).content
```

上述代码所完成的操作仅仅就是
- 1、打开网络流；
- 2、读取返回的内容。

为了突出重点，这里省略了代理、Header、以及超时的设置。但这样做不能分辨出假死的情况，尤其是微博这种视频图片居多的网站，很有可能卡在抓取视频图片的过程中不动。或者在下载大文件的时候，虽然文件一直在下载，但我们却不知道文件到底下载了多少，还有多少时间。

所以在爬虫开发过程中，如果能动态的展示视频或图片的下载过程对于监控爬虫运行时非常必要的。
 
![](/imgs/xunlei.png)
图表 1 迅雷下载中的进度条
### 2.正文	
要做到为下载过程添加进度条，首先需要了解requests.get()方法和tqdm包。
#### 2.1 tqdm包
tqdm来自阿拉伯文taqaddum ，意思是进度，也是西班牙语中的te quiero demasiado缩写，意思是我非常爱你。
#### 2.1.1 安装的方式
```
conda install -c conda-forge tqdm
pip install tqdm
```
#### 2.1.2 使用
tqdm使用起来也非常方便，最简单的用法如下：
```
from tqdm import tqdm#导入相应的方法
for i in tqdm(range(10000)):#tqdm()方法
	pass
```
只需要引入tqdm方法，然后使用将可迭代（iterable）的对象传入tqdm（）方法即可。

复杂一点的用法如下：
```
with tqdm(total=100) as pbar:#tqdm方法设置进度条长度
    for i in range(10):
        sleep(0.1)
        pbar.update(10)#手动更新进度
```
#### 2.2 requests
#### 2.2.1 get
本文获取文件长度通过requests.get()方法。Requests.get()方法当stream=True的时候，get()方法只下载Header部分，如果要下载Body部分，需要读取content属性才会下载。所以我们可以利用这一点来完成对视频图片的下载监控。获取文件大小的方法如下：
```
response=requests.get(img_url,stream=True)
file_size=response.headers['Content-length']
```
#### 2.2.2 iter_content
Iter_content方法用于分块读取get()方法返回的流，避免因一次性读取消耗大量内存。

### 3.为视频图片下载添加进度条
完整的代码如下：
```
import requests
import tqdm
img_url='http://122.51.50.206:8088/imgs/63943f53ly1gjgojmh9zaj222o0yi7wq.jpg'
response=requests.get(img_url,stream=True)
file_size=response.headers['Content-length']
print(file_size)
pbar=tqdm.tqdm(total=int(file_size),unit='B',unit_scale=True,desc=img_url.split('/')[-1])
with(open('1.jpg','wb')) as f:
    for chunk in response.iter_content(chunk_size=1024):
        if  chunk:
            f.write(chunk)
            pbar.update(1024)
pbar.close()
```
步骤如下：
（1）	获取Header
（2）	读取Header中的Content-length字段得到文件大小
（3）	初始化tqdm
（4）	分块读取文件并更新进度条
（5）	关闭进度条

最后，欢迎持续关注。

![](/imgs/1602143592.png)
