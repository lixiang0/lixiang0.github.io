---
title: "[Gensim]5.Word2Vec"
category: Gensim
layout: post
date: '2017-12-26 20:56:24'
---
```

# import modules & set up logging
import gensim, logging



logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)

#build for sentences list
sentences = [['first', 'sentence'], ['second', 'sentence']]
# train word2vec on the two sentences
model = gensim.models.Word2Vec(sentences, min_count=1,workers=4)

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

#model save and load
model.save('/tmp/mymodel')
new_model = gensim.models.Word2Vec.load('/tmp/mymodel')
model = gensim.models.Word2Vec.load_word2vec_format('/tmp/vectors.txt', binary=False)
# using gzipped/bz2 input works too, no need to unzip:
model = gensim.models.Word2Vec.load_word2vec_format('/tmp/vectors.bin.gz', binary=True)



#usage
model.most_similar(positive=['woman', 'king'], negative=['man'], topn=1)
#[('queen', 0.50882536)]
model.doesnt_match("breakfast cereal dinner lunch".split())
'cereal'
model.similarity('woman', 'man')
#0.73723527
```
