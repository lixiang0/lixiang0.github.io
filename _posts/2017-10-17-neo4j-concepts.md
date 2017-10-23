---
title: "[neo4j]2.Neo4j相关概念"
catagories: neo4j
layout: post
date: '2017-10-17 21:30:24'
---


### 1.Neo4j graph database
简单的Neo4j数据库的样子：
<br>![]({{ "/imgs/20171023-213314.png" | absolute_url }})<br>
### 2.Node：
最简单的一个Node就像下面的样子：

<br>![]({{ "/imgs/20171023-213602.png" | absolute_url }})<br>
再新建2个节点并为每一个节点添加一个属性。

<br>![]({{ "/imgs/20171023-214046.png" | absolute_url }})<br>

### 3.Relationship
关系是图数据库的一个核心特性。关系连接2个节点，一个是源节点，一个是目标节点。正因为有了关系才使得节点构成了丰富又复杂的结构，可以是：列、树或者复合行的实体。

<br>![]({{ "/imgs/20171023-215632.png" | absolute_url }})<br>

上图中关系类型有：```ACTED_IN```和```DIRECTED```。关系```ACTED_IN```的属性```roles```值为一个数组。
对于```ACTED_IN```关系来说，节点```Tom Hanks```是源节点，``` Forrest Gump ```是目标节点。我们可以这么形容：节点```Tom Hanks```有一个指向关系，``` Forrest Gump ```有一个被指向关系。
关系的方向在搜索的时候是等价的，也就是说是双向的。
关系还可以指向节点自身。

<br>![]({{ "/imgs/20171023-220159.png" | absolute_url }})<br>

这表示着Tom Hanks KNOWS 他自己。
对于图：

<br>![]({{ "/imgs/20171023-220311.png" | absolute_url }})<br>

可以得到下表：

<br>![]({{ "/imgs/20171023-220358.png" | absolute_url }})<br>

### 4.属性
属性具有属性名和值，属性名是一个string，值的类型是：

- 数字
- 字符串
- 布尔值
- 上述类型的list

下图是一个示例：

<br>![]({{ "/imgs/20171023-221028.png" | absolute_url }})<br>

### 5.Label
Label对节点进行标记分成不同的集合。比如对于银行账户标记为```:Suspended```就表示这是封存的账户，对蔬菜标记```:Seasonal```就表示是当季的。
下面是一个示例：

<br>![]({{ "/imgs/20171023-221638.png" | absolute_url }})<br>

节点也可以有多个label：

<br>![]({{ "/imgs/20171023-221704.png" | absolute_url }})<br>

注意节点的label是非空的，命名的时候使用驼峰命名法，比如CarOwner.


### 6.Traversal
图的查询是从一个节点出发，然后查找符合既定规则的关系。Cypher就是用于图查询的类似SQL语言，本文就不再赘述，下文再进行介绍。
