---
title: "[NLP]训练Word2vec的JAVA版本"
layout: post
date: '2017-07-28 19:33:52 +0800'
catagories: nlp
---

## 前言
word2vec是什么在这里就不再赘述了，简单的说就是将词组转换成向量，完成词组的数值化表示。本文的目标是完成word2vec的java版本的训练。系统系统环境为ubuntu 14.04 64位。

## 过程

### 1.命令行执行：
```
git clone https://github.com/NLPchina/Word2VEC_java.git
cd Word2VEC_java
```
### 2.
在Word2VEC_java目录下新建library目录，然后下载[语料](https://pan.baidu.com/s/1eSxIVwm)到这个路径下。
### 3.
修改Word2VEC_java/src/main/java/com/ansj/vec/Learn.java文件中的main函数为：
```
    Learn learn = new Learn();
    long start = System.currentTimeMillis();
    learn.learnFile(new File("library/xh.txt"));
    System.out.println("use time " + (System.currentTimeMillis() - start));
    learn.saveModel(new File("library/javaVector.model"));
```
### 4.训练
在文件根目录执行：
```
export MAVEN_OPTS="-Xms12000m -Xmx12000m -XX:MaxPermSize=1024m"//防止出现内存溢出
mvn -X compile
mvn -X clean install exec:java -Dexec.mainClass="com.ansj.vec.Learn"
```
执行之后可以看到如下输出：
```
alpha:0.02044900416390071	Progress: 18%
alpha:0.020447493168044915	Progress: 18%
alpha:0.02044602730716377	Progress: 18%
alpha:0.020444000483026293	Progress: 18%
alpha:0.020442504434467296	Progress: 18%
alpha:0.020441011609835063	Progress: 18%
alpha:0.02043928549013907	Progress: 18%
alpha:0.02043781962925792	Progress: 18%
alpha:0.020436076950301748	Progress: 18%
```
以上就完成了本文的目标，生成的模型文件路径为：library/javaVector.model。
训练之后，下一步的目标就是进行得到词向量之后计算句向量了，这就是后文的目标了。