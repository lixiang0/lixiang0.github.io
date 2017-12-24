---
title: "[Gensim]2.Corpora and Vector Spaces"
catagories: Gensim
layout: post
date: '2017-12-24 19:16:24'
---
```
import logging


logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)


# 加载语料库
documents =[line.split('$$$')[0] for line in open('../data/corpus.txt','r').readlines()]
print(documents[:5])

# 移除停用词
stopwords='啊呢吗的'
texts=[[word for word in document if word not in stopwords]  for document in documents]
print(texts[:5])

# 构造词频
from collections import defaultdict
freq=defaultdict(int)
for text in texts:
    for word in text:
        freq[word]+=1
# 移除出现次数少于1次的词
texts=[ [word for word in text if freq[word]>1] for text in texts]
print(texts[:5])

# 构造词典
from gensim import corpora
dictionary=corpora.Dictionary(texts)
print(dictionary)
print(dictionary.token2id)

# 本地持久化
dictionary.save('./model/dictionary.m')

# 文档向量化
new_text='今天天气比较好，适合出去旅游'
new_vec=dictionary.doc2bow(list(new_text))
print(new_vec)


# 文档序列化
corpus=[dictionary.doc2bow(text) for text in texts]

corpora.MmCorpus.serialize('./model/corpra.mms',corpus)
corpus = corpora.MmCorpus('/tmp/corpus.mms')

corpora.SvmLightCorpus.serialize('/tmp/corpus.svmlight', corpus)
corpus = corpora.SvmLightCorpus('/tmp/corpus.svmlight')

corpora.BleiCorpus.serialize('/tmp/corpus.lda-c', corpus)
corpus = corpora.BleiCorpus('/tmp/corpus.lda-c')

corpora.LowCorpus.serialize('/tmp/corpus.low', corpus)
corpus = corpora.LowCorpus('/tmp/corpus.low')

# memory friendly 1
class MyCorpus:
    def __iter__(self):
        for line in open('../data/corpus.txt','r'):
            yield dictionary.doc2bow(list(line))
corpus_friendly=MyCorpus()

# memory friendly 2
from six import iteritems
once_ids = [tokenid for tokenid, docfreq in iteritems(dictionary.dfs) if docfreq == 1]#document frequencies: tokenId -> in how many documents this token appeared

#corpus compacty
dictionary.filter_tokens(once_ids)#remove id=1
dictionary.compactify()#remove gaps between id
```