---
title: "3.Topic and Transformations"
category: nlp
layout: post
tags: [Gensim,nlp]
date: '2017-12-25 20:56:24'
---
```
import logging
logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)


from gensim import corpora,models,similarities
import os
if os.path.exists('./model/dictionary.m'):
    dictionary=corpora.Dictionary.load('./model/dictionary.m')
    print(dictionary)
    corpus=corpora.MmCorpus('./model/corpra.mms')
    print('load dictionary and corpus done')
    #build tf-idf model
    tfidf_model=models.TfidfModel(corpus=corpus, normalize=True)
    tfidf_corpus=tfidf_model[corpus]
    # for corpra in tfidf_corpus:
    #     print(corpra)
    #build lsi model
    lsi_model=models.LsiModel(corpus=tfidf_corpus,id2word=dictionary,num_topics=4)
    lsi_corpus=lsi_model[corpus]
    # for corpra in lsi_corpus:
        # print(corpra)
    print(lsi_model.show_topics(2))
    # lsi_model.add_documents([])#add new document
    # lsi_vec = lsi_model[]#transform to vector
    #random projection model
    rp_model = models.RpModel(tfidf_corpus, num_topics=500)
    #latent Dirichlet Allocation
    lda_model = models.LdaModel(tfidf_corpus, id2word=dictionary, num_topics=100)
    #Hierarchical Dirichlet Process
    hdp_model = models.HdpModel(tfidf_corpus, id2word=dictionary)
else:
    print('file not exsit')
```
