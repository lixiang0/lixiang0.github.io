---
title: "如何使用Mongoengine保存文件"
category: python
layout: post
tags: [python]
date: '2020-01-08 14:00:24'
---

# 引言
因为文件大小的限制，mongodb中通常使用GridFS进行文件存储。MongoEngine是python中实现对象-文档的映射的包。它基于GridFS提供了用于文件存储的FileField对象，并且文件的操作和python内置文件操作一样。

FileField提供Write、Read、Delete、Replace四种操作。FileField在GridFS中将保存在一个文件中。如果想要覆盖原文件，那么需要进行删除和创建新文件的操作。FileField和文件系统类似，但是一个明显的区别是FileField只能写一次。


# 使用方法


```
from mongoengine import Document
from mongoengine import FileField

class Article(Document):
    # collection_name参数默认为'fs'，当然也可以自定义。
    # 自定义方式：FileField(collection_name='images')
    upload = FileField()

art = Article()
with open('image.png', 'rb') as image_file:
    art.upload.put(image_file, content_type='image/png')

# 如果是网络读取文件，则需要用到StringIO或者使用临时文件
mem_file = StringIO()
mem_file.write(image_content_from_http)
art.upload.put(mem_file, content_type='image/png')

#如果要替换文件则
with open('image.png', 'rb') as image_file:
    art.upload.replace(image_file, content_type='image/png')
```
# FileField提供的方法

- get
- new_file
- put
- replace
- write
- writelines
- close
- replace
如果要进行写操作使用```write```操作，如果是进行读操作，则使用```read```操作；如果是进行```replace```操作，则需要先进行```delete```操作，然后使用```write```或者```new_file```。注意使用```write```方法之后记得执行```close```操作对流进行关闭。


# list操作

有时候需要进行多文件的读写，比如一次写入多张图片，下面给出一个例子：
```
from mongoengine import Document
from mongoengine import FileField, EmbeddedDocument, EmbeddedDocumentField


class ArticleImage(EmbeddedDocument):
    image = FileField()


class Article(Document):
    images = ListField(EmbeddedDocumentField(ArticleImage))


art = Article()
image_1 = ArticleImage()
with open('image1.png', 'rb') as image_file:
    image_1.put(image_file, content_type='image/png')
image_2 = ArticleImage()
with open('image2.png', 'rb') as image_file:
    image_2.put(image_file, content_type='image/png')

art.images.append(image_1)
art.images.append(image_2)

#读
for img in Article.objects():
    pass
```