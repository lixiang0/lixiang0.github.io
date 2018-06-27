---
title: "5.Word2Vec"
category: nlp
layout: post
tags: [Gensim,nlp]
date: '2017-12-26 20:56:24'
---
最简单的word2vec训练方式：
```
# import modules & set up logging
import gensim
#build for sentences list
sentences = [['first', 'sentence'], ['second', 'sentence']]
# train word2vec on the two sentences
model = gensim.models.Word2Vec(sentences, min_count=1,workers=4)
```
如果文本太多，可以使用一种优化内存的加载方法：
```
#build from files
import os

class MemorySentences(object):
    def __init__(self,path):
        self.path=path
    def __iter__(self):
        for filename in os.listdir(self.path):
            for line in open(os.path.join(self.path,filename),'r'):
                yield list(line)
corpus=MemorySentences('../data/wiki_zh/')
model = gensim.models.Word2Vec(corpus, min_count=1,workers=4)
```
模型的保存和加载：
```
#model save and load
model.save('/tmp/mymodel')
new_model = gensim.models.Word2Vec.load('/tmp/mymodel')
model = gensim.models.Word2Vec.load_word2vec_format('/tmp/vectors.txt', binary=False)
# using gzipped/bz2 input works too, no need to unzip:
model = gensim.models.Word2Vec.load_word2vec_format('/tmp/vectors.bin.gz', binary=True)
```
使用方法：
```
#usage
model.most_similar(positive=['woman', 'king'], negative=['man'], topn=1)
#[('queen', 0.50882536)]
model.doesnt_match("breakfast cereal dinner lunch".split())
'cereal'
model.similarity('woman', 'man')
#0.73723527
```
