---
title: "docker使用简明教程"
category: python
layout: post
tags: [other,docker]
date: '2021-01-09 00:00:24'
---



最近项目需要使用了Docker，结果在使用了之后就停不下来。
Docker对于自动化部署来说真真太方便了。

## docker是什么

简而言之，docker是一个用于开发、分发和测试、生产的平台。它最大的优势在于：能够迅速自动化的部署开发的应用。Docker相当于在宿主机上虚拟出了N个独立的应用运行环境，每个应用的环境都是独立的，每个应用也是独立的。

![](https://docs.docker.com/engine/images/engine-components-flow.png)

从上图可以看出，Docker的主要包括：

- （1）Server：用于运行docker主程，并常驻内存。
- （2）REST API：用于与server进行交互
- （3）CLI（command line interface）：docker的命令（比如docker build），有了CLI就可以与server通过命令行进行交互。


## 两个重要的概念

### images
images是Docker中重要的概念之一，相当于Windows的ISO镜像，可以用于安装Windows系统。
比如：```docker pull ubuntu```相当于拉取一个ubuntu系统的镜像到本地。可以通过命令行执行''docker images''查看本地拥有哪些镜像。

### container
container也是Docker中重要的概念之一，相当于安装好了的Windows系统，可以start、pause、stop、restart。比如：```docker run ubuntu```相当于安装并启动一个ubuntu系统。通过命令行执行''docker ps -a''查看所有的容器。

这两个概念在开始的时候不好理解，但是以操作系统的ISO镜像和操作系统去类比会好理解得多。

## 使用docker

### 安装

docker在Ubuntu系统中的安装比较简单，只需要执行下面的命令即可：

```
sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

sudo docker run hello-world
```
当看到如下输出：

```
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete 
Digest: sha256:1a523af650137b8accdaed439c17d684df61ee4d74feac151b5b337bd29e7eec
Status: Downloaded newer image for hello-world:latest

Hello from Docker!

```
即表示安装成功了。


### 使用

常用命令：
- attach      Attach local standard input, output, and error streams to a running container
- build       根据Dockerfile文件创建镜像
- commit      Create a new image from a container's changes
- cp          在容器和宿主机之前拷贝文件
- create      创建一个新容器
- diff        Inspect changes to files or directories on a container's filesystem
- events      Get real time events from the server
- exec        Run a command in a running container
-  export      Export a container's filesystem as a tar archive
-  history     Show the history of an image
-  images      列出所有的镜像
-  import      从本地导入镜像
-  info        Display system-wide information
-  inspect     Return low-level information on Docker objects
-  kill        Kill one or more running containers
-  load        Load an image from a tar archive or STDIN
-  login       Log in to a Docker registry
-  logout      Log out from a Docker registry
-  logs        Fetch the logs of a container
-  pause       Pause all processes within one or more containers
-  port        List port mappings or a specific mapping for the container
-  ps          列出所有的容器
-  pull        从仓库中拉取镜像
-  push        将镜像推送到镜像
-  rename      重命名容器
-  restart     重启容器
-  rm          删除一个或多个容器
-  rmi         删除一个或多个镜像
-  run         启动一个新容器
-  save        Save one or more images to a tar archive (streamed to STDOUT by default)
 - search      Search the Docker Hub for images
-  start       Start one or more stopped containers
-  stats       Display a live stream of container(s) resource usage statistics
-  stop        Stop one or more running containers
-  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
-  top         Display the running processes of a container
-  unpause     Unpause all processes within one or more containers
 - update      Update configuration of one or more containers
- version     Show the Docker version information
- wait        Block until one or more containers stop, then print their exit codes

如果对命令有疑问可以通过```docker --help```命令查看命令的使用。

## 一个例子


### 1.新建文件Dockerfile

新建目录test/，然后新建Dockerfile文件，内容如下：

```
FROM ubuntu:18.04
WORKDIR /code

#RUN 执行命令
RUN apt update --yes && apt upgrade --yes 

# 安装python
RUN  apt-get install python-dev --yes

COPY . .

# 执行web.py
CMD ["python","web.py"]
```

### 2.新建web.py文件

web.py文件中写入如下内容：
```
print('hello')

```

### 2.新建镜像

```
docker built -t test .
```
可以看到输出：
```
Step 17/18 : COPY . .
 ---> 1ba374f5a1d2
Step 18/18 : CMD ["python","web.py"]
 ---> Running in 365d4b7fd252
Removing intermediate container 365d4b7fd252
 ---> 5403a172511d
Successfully built 5403a172511d
Successfully tagged test:latest
```
表示成功新建了镜像。

### 3.新建容器

```
$ sudo docker run test
hello
```
可以看到``hello``就是容器的输出，表明容器新建成功。

