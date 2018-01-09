---
title: "3.RNN模型"
category: dl
layout: post
tags: [Pytorch,dl]
date: '2018-01-08 17:10:24'
---


本文的目标是实现Elman RNN模型。

### Elman RNN模型
模型结构用数学公式表示很简单：

$$h_t=\tanh(w_{ih}*x_t+b_{ih}+w_{hh}*h_{(t-1)}+b_hh)$$

$h_{(t-1)}$表示$t-1$时刻隐层的输出，$x_t$表示$t$时刻的输入,i表示第i层。RNN使用tanh或ReLU作为激活函数。

模型的结构如下图所示：

![](/imgs/rnn.png)

### Pytorch中的RNN模型

Pytorch中RNN模型的API为：
```python
class torch.nn.RNN(*args, **kwargs)
```
#### 1.构造函数参数说明:	

|参数|说明|
|-|-|
|input_size|输入层输入的特征个数|
|hidden_size|隐层输入的特征个数|
|num_layers|网络的层数|
|nonlinearity|非线性激活函数：‘tanh’或’relu’. 默认: ‘tanh’|
|bias|False,表示偏置值为0, 默认: True|
|batch_first|True, 表示输入、输出中batch放在参数第一个：(batch, seq, feature)|
|dropout|非0表示引入Drop层，最后一层除外。|
|bidirectional|True, 表示双向RNN. 默认: False|


#### 2.输入参数说明：

- input：输入的格式(seq_len, batch, input_size)
- $h_0$：训练开始时隐层的初始状态：$h_0 (num_layers * num_directions, batch, hidden_size)$

batch表示有几个长度为seq_len的序列。

#### 3.输出参数说明: 

- output：输出的格式：$output(seq_len, batch,  hidden_size* num_directions)$
- $h_n$：n时刻隐层的输出：$h_n (num_layers * num_directions, batch, hidden_size)$


#### 4.中间变量

|参数|说明|
|-|-|
|weight_ih_l[k]|模型学习到第k个输入层到隐层的参数，大小为：(input_size x hidden_size)|
|weight_hh_l[k]|模型学习到第k个隐层到隐层的参数，大小为：(hidden_size x hidden_size)|
|bias_ih_l[k]|模型学习到第k个输入层到隐层的偏置参数，大小为： (hidden_size)|
|bias_hh_l[k]|模型学习到第k个隐层到隐层的偏置参数，大小为： (hidden_size)|

#### 5.实例

```
rnn = nn.RNN(10, 20, 2)
input = Variable(torch.randn(5, 3, 10))
h0 = Variable(torch.randn(2, 3, 20))
output, hn = rnn(input, h0)
```


#### 6.RNN用于字符串分类的实例


##### 数据准备
```python
# data process
import os
import numpy as np

print(os.getcwd())
lines = open('../data/cnn_paris.txt').readlines()
print(len(lines))
input_size=10 #输入的特征
hidden_size=20#隐层的特征
num_layers=2 #rnn的层数
embedding_size = 256
word2index = dict()
index2word = dict()
clss2index = dict()
index2clss = dict()
texts = []
clss = []
max_len = 0
for line in lines:
    #文本格式为：类别$$问题$$回答
    arrs = line.split('$$')
    clss.append(arrs[0])
    texts.append(arrs[1])
    if max_len < len(arrs[1]):
        max_len = len(arrs[1])
    for arr in arrs:
        for word in arr:
            if word not in word2index:
                word2index[word] = len(word2index)
                index2word[len(word2index)] = word
    if arrs[0] not in clss2index:
        clss2index[arrs[0]] = len(clss2index)
        index2clss[len(clss2index)] = arr[0]
print(len(word2index))
print(len(index2word))
print(len(clss2index))
print(len(index2clss))
print(str(max_len))
texts_array = np.zeros(shape=(len(texts), max_len))
for i, text in enumerate(texts):
    for j, word in enumerate(text):
        texts_array[i][j] = word2index[word]
clss_array = np.zeros(shape=(len(texts), 1))
for i, cls in enumerate(clss):
    clss_array[i] = clss2index[cls]
print(texts_array[0])

embedded = torch.nn.Embedding(len(word2index), input_size)


def embedding(seq):
    return embedded(seq)
```
##### 模型构建
```python
import torch
# 输入为(seq_len,embedding_size)，经过RNN之后连接到一个感知器，再经过softmax层输出分类结果
# classification model
class RNNModel(torch.nn.Module):
    def __init__(self, input_features, hidden_features, num_layers, bi, class_nums):
        super(RNNModel, self).__init__()
        self.num_layers = num_layers
        self.bi = bi
        self.hidden_features = hidden_features
        self.class_nums = class_nums
        print('input_features', input_features, 'hidden_features', hidden_features, 'num_layers', num_layers, bi,
              'class_nums', class_nums)
        self.rnn = torch.nn.RNN(input_features, hidden_features, num_layers, bidirectional=bi, batch_first=True,dropout=0.2)
        self.softmax = torch.nn.Softmax()

    def forward(self, input_seq):
        self.h0 = torch.autograd.Variable(
            torch.randn(self.num_layers * (self.bi + 1), len(input_seq), self.hidden_features))
        self.linear = torch.nn.Linear((self.bi + 1) * self.hidden_features * input_seq.size()[1], self.class_nums)
        self.linear.cuda()
        out_rnn, _ = self.rnn(input_seq, self.h0.cuda())
        out_rnn = out_rnn.view(out_rnn.contiguous().size()[0], -1)
        out_rnn=out_rnn.view(out_rnn.size()[0], -1).cuda()
        out_linear = self.linear(out_rnn)
        out_softmax = self.softmax(out_linear)
        return out_softmax
```


##### 模型训练
```python
model = RNNModel(input_size, hidden_size, num_layers, False, 10)
model.cuda()
x = embedding(torch.autograd.Variable(torch.from_numpy(texts_array.astype('int')).view(len(texts_array), max_len)))
y = torch.autograd.Variable(torch.from_numpy(clss_array.astype('int')).view(len(clss_array)), requires_grad=False)
print('x', x.size())
print('y', y.size())

optimizer = torch.optim.SGD(model.parameters(), lr=0.1)
loss_fun = torch.nn.NLLLoss()
batch_size=30
batchs=int(len(x)/batch_size)

try:
    epoch=0
    while(True):
        epoch += 1
        loss_sum=0.0

        for batch in range(batchs):
            correct = 0
            model.zero_grad()
            x_train=x[batch*batch_size:(batch+1)*batch_size].cuda()
            y_train = y[batch*batch_size:(batch+1)*batch_size].cuda()
            y_pred=model(x_train)
            loss=loss_fun(y_pred,y_train)
            loss.backward(retain_variables=True)
            optimizer.step()
            loss_sum+=loss.data[0]
            for i in range(batch_size):
                # print(torch.max(y_pred.data, 1)[1][i][0],y.data[i] )
                if torch.max(y_pred.data, 1)[1][i]==y.data[i] :
                    correct += 1
            print('epoch=',epoch,'loss=',loss.data[0],' accuracy=',correct/batch_size)
except KeyboardInterrupt:
    print('key interrupt...')
finally:
    torch.save(model,'./model/nlp_classification_rnn.model')
```
