---
title: "如何部署分布式框架Celery到远程机器上"
category: python
layout: post
tags: [python]
date: '2019-11-12 16:00:24'
---

最近做了一个抢票软件用于抢票，开发好了之后分布在4台服务器上运行。实际的开发和部署过程有点繁琐，所以萌生了基于分布式的想法。
了解到python中Celery框架使用得较多，因而本文就学习一下如何部署基于Celery的代码到远程机器上。

### Celery中的三个组件
Celery的思想比较简单，就是一个基于消息的分布式框架。核心有三个组件：

- Application: 类似于客户端像服务器不断的请求执行新的任务；
- Worker: 类似于服务器，用于执行任务；
- Broker: 负责通信。

这三个组件组成了Celery的核心部分，一方面客户端不需要了解服务器的实现，只需要通过Broker发送消息即可;
另一方面服务器只需要关心具体的业务，Broker只负责通信。

下面开始逐步搭建一个远程Celery服务。

### 0、安装必要的包
```
#安装erlang
wget http://packages.erlang-solutions.com/site/esl/esl-erlang/FLAVOUR_1_general/esl-erlang_20.1-1~ubuntu~xenial_amd64.deb
sudo dpkg -i esl-erlang_20.1-1\~ubuntu\~xenial_amd64.deb

#安装rabbitmq
echo "deb https://dl.bintray.com/rabbitmq/debian xenial main" | sudo tee /etc/apt/sources.list.d/bintray.rabbitmq.list
wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install rabbitmq-server
sudo systemctl start rabbitmq-server.service
sudo systemctl enable rabbitmq-server.service

#安装Celery
pip install celery
```

### 第一步：添加用户

这一步需要在服务器中进行，添加的目的类似于在服务器添加一个账户，这样就使得客户端能够使用这个账户访问服务器的权限。
```
# 添加帐号密码
sudo rabbitmqctl add_user <user> <password>

# 添加虚拟主机
sudo rabbitmqctl add_vhost <vhost_name>

# 添加权限
sudo rabbitmqctl set_permissions -p <vhost_name> <user> ".*" ".*" ".*"

# 重启
sudo rabbitmqctl restart
```

### 第二步：编写服务器代码server.py
```
from celery import Celery

app = Celery('tasks', backend='amqp',
broker='amqp://<user>:<password>@<ip>/<vhost>')

def add(x, y):
return x + y
```
并在服务器执行：
```
celery -A server worker --loglevel=info
```

### 第三步：编写客户端代码

#### 1.task.py
```
from server import add
result = add.delay(4, 4)
print(result.get(timeout=1))
```

#### 2.server.py
```
from celery import Celery
app = Celery('server',backend = 'rpc://',broker='amqp://<user>:<password>@<ip>/<vhost>')
@app.task
def add(x, y):
    # return x + y
    pass
```
并在客户端执行：
```
python task.py
```
即可看到本地输出：
```
8
```

服务器输出：
```
[2019-11-12 16:18:06,145: INFO/MainProcess] Received task: server.add[0455eccf-b81e-46d4-9b19-b511d8e1a93e]  
[2019-11-12 16:18:06,147: INFO/ForkPoolWorker-1] Task server.add[0455eccf-b81e-46d4-9b19-b511d8e1a93e] succeeded in 0.0005705989897251129s: 8
```

以上。
