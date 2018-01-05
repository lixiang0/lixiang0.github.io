---
title: "4.Similarity and Queries"
category: Gensim
layout: post
tags: [Gensim]
date: '2017-12-25 21:27:24'
---

```
import logging


logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)

from gensim import corpora,models,similarities

import os
if os.path.exists('./model/dictionary.m'):
    dictionary=corpora.Dictionary.load('./model/dictionary.m')
    corpus=corpora.MmCorpus('./model/corpra.mms')

    lsi_model=models.LsiModel(corpus=corpus,id2word=dictionary,num_topics=5)
    doc='你今天心情怎么样'
    vec_doc=dictionary.doc2bow(list(doc))
    vec_lsi=lsi_model[vec_doc]
    print(vec_lsi)


    #build similarity matrix
    sim_matrix=similarities.MatrixSimilarity(lsi_model[corpus])
    sim_matrix.save('./model/lsi_sim.m')
    del(sim_matrix)
    sim_matrix=similarities.MatrixSimilarity.load('./model/lsi_sim.m')
    sims=sim_matrix[vec_lsi]
    sims = sorted(enumerate(sims), key=lambda item: -item[1])
    print(sims)

```
