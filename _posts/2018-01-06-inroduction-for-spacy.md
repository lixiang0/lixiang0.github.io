---
title: "spaCy的简易教程"
category: nlp
layout: post
tags: [spacy,nlp]
date: '2018-01-06 14:30:24'
---

spaCy是一个NLP工具包用于完成NLP领域的很多任务比如词性标注，命名实体识别等，支持Unix/Linux,macOS/os X和Windows操作系统，可以通过pip,conda方式安装。

pip:

```
pip install -U spacy
```
conda:

```
conda install -c conda-forge spacy
```

### 支持的语言：


|NAME	|LANGUAGE	|TYPE
|--|--|
|en_core_web_sm	|English	|Vocabulary, syntax, entities|
|en_core_web_md	|English	|Vocabulary, syntax, entities, vectors|
|en_core_web_lg	|English	|Vocabulary, syntax, entities, vectors|
|en_vectors_web_lg	|English	|Word vectors|
|de_core_news_sm|	German	|Vocabulary, syntax, entities|
|es_core_news_sm|	Spanish	|Vocabulary, syntax, entities|
|es_core_news_md|	Spanish	|Vocabulary, syntax, entities, vectors|
|pt_core_news_sm|	Portuguese|	Vocabulary, syntax, entities|
|fr_core_news_sm|	French	|Vocabulary, syntax, entities|
|fr_core_news_md|	French	|Vocabulary, syntax, entities, vectors|
|it_core_news_sm|	Italian	|Vocabulary, syntax, entities|
|nl_core_news_sm|	Dutch	|Vocabulary, syntax, entities|
|xx_ent_wiki_sm	|Multi-language	|Named entities|

###  语言模型
[语言模型](https://github.com/explosion/spacy-models)的安装：
```
#命令行
python -m spacy download xx
#pip
pip install https://github.com/explosion/spacy-models/releases/download/en_core_web_md-1.2.0/en_core_web_md-1.2.0.tar.gz
#本地文件
pip install /Users/you/en_core_web_md-1.2.0.tar.gz

```

安装语言模型之后就可以在代码中使用了：
```
import spacy
nlp = spacy.load('en')                       # load model with shortcut link "en"
nlp = spacy.load('en_core_web_sm')           # load model package "en_core_web_sm"
nlp = spacy.load('/path/to/en_core_web_sm')  # load package from a directory

doc = nlp(u'This is a sentence.')
```

安装中如果遇到问题参考[链接](https://spacy.io/usage/)

### 用法

[词性标注](https://spacy.io/usage/linguistic-features#section-pos-tagging)：
```
doc = nlp(u'Apple is looking at buying U.K. startup for $1 billion')

for token in doc:
    print(token.text, token.lemma_, token.pos_, token.tag_, token.dep_,
          token.shape_, token.is_alpha, token.is_stop)
```

[依存树](https://spacy.io/usage/linguistic-features#dependency-parse)：
```
doc = nlp(u'Autonomous cars shift insurance liability toward manufacturers')
for token in doc:
    print(token.text, token.dep_, token.head.text, token.head.pos_,
          [child for child in token.children])
```

[命名实体识别](https://spacy.io/usage/linguistic-features#named-entities):
```
doc = nlp(u'Apple is looking at buying U.K. startup for $1 billion')

for ent in doc.ents:
    print(ent.text, ent.start_char, ent.end_char, ent.label_)
```

[标签化](https://spacy.io/usage/linguistic-features#tokenization):
```
for token in doc:
    print(token.text)
```

