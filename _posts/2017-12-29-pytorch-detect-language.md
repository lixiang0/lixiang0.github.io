---
title: "[Pytorch]2.Detect Language"
catagories: Pytorch
layout: post
date: '2017-12-29 18:10:24'
---

```
import torch
import torch.nn as nn
import torch.autograd as autograd
import torch.functional as F

data = [("我 的 家 乡 在 哪 里".split(), "CHINESE"),
        ("Give it to me".split(), "ENGLISH"),
        ("今 天 天 气 怎 么 样".split(), "CHINESE"),
        ("No it is not a good idea to get lost at sea".split(), "ENGLISH")]

test_data = [("天 气 在 哪 里".split(), "CHINESE"),
             ("it is lost on me".split(), "ENGLISH")]
word2index={}
for sen,_ in data+test_data:
    for word in sen:
        if word not in word2index:
            word2index[word]=len(word2index)
print(word2index)
VOCAB_SIZE=len(word2index)
NUM_CLASSES=2
label2index={'CHINESE':0,'ENGLISH':1}

class BoWClassifier(torch.nn.Module):
    def __init__(self,num_labels,vocab_size):
        super(BoWClassifier,self).__init__()
        self.linear=nn.Linear(vocab_size,num_labels)
        self.softmax=nn.Softmax()
    def forward(self,bow_vec):
        return self.softmax(self.linear(bow_vec))
def make_bow_vector(sentence,word2index):
    vec=torch.zeros(len(word2index))
    for word in sentence:
        vec[word2index[word]]+=1
    return vec.view(1,-1)
def make_target(label,label2index):
    return torch.LongTensor([label2index[label]])

model=BoWClassifier(NUM_CLASSES,VOCAB_SIZE)

# for param in model.parameters():
#     print(param)
log_prob=model(autograd.Variable(make_bow_vector(data[0][0],word2index)))
print(log_prob)

loss_function=nn.NLLLoss()
optimizer=torch.optim.SGD(model.parameters(),lr=0.1)

for epoch in range(100):
    for instance,label in data:
        model.zero_grad()
        bow_vec=autograd.Variable(make_bow_vector(instance,word2index))
        target=autograd.Variable(make_target(label,label2index))
        # print(target)
        log_prob=model(bow_vec)
        # print(log_prob)
        loss=loss_function(log_prob,target)
        loss.backward()
        optimizer.step()
for instance,label in test_data:
    bow_vec=autograd.Variable(make_bow_vector(instance,word2index))
    log_prob=model(bow_vec)
#     print(log_prob)
print(model(autograd.Variable(make_bow_vector(['Give','good','good','good','good'],word2index))))
```