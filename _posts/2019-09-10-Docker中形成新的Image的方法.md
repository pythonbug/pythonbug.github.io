---
layout: post
title:  "Docker中形成新的image的两种方法"
date:   2019-09-10 22:47
categories: Docker
tags: images
excerpt: 知识点记录
author: Pythonbug
mathjax: true
---

## docker commit的方法
#### Step 1: 拉取基础镜像
```
docker pull centos
```

#### Step 2: 交互式的方式运行容器
```
docker run -it centos
```

#### Step 3: 安装vim（一开始的centos镜像不带vim）
```
yum install vim
```

#### Step 4: 退出交互式，在原先容器的基础上新建镜像
```
exit
# 查看刚刚退出的容器号
docker ps -a
# 获取CONTAINER ID,此处的35a3fd04e44d为我自己的容器ID
docker commit 35a3fd04e44d pythonbug/centos-vim
```

#### Step 5: 查看新生成的镜像
```
docker images
```
![](https://github.com/pythonbug/myPictures/blob/master/QQ%E6%88%AA%E5%9B%BE20190910231227.png?raw=true)

## Dockerfile的方法（推荐）
#### Step 1: 创建目录
```
mkdir centos-vim
```

#### Step 2: 编辑Dockerfile
```
cd centos-vim/
vim Dockerfile
## 内容如下
FROM centos
RUN yum -y install vim
```

#### Step 3: docker build
```
docker build -t pythonbug/centos-vim2 .
```

#### Step 4: 查看一下
```
docker images
```

## 为什么推荐使用Dockerfile的原因
<video id="video" controls="" preload="none" source id="mp4" src="https://my-blog-video.oss-cn-shanghai.aliyuncs.com/Docker/%E4%BD%BF%E7%94%A8Dockerfile%E8%80%8C%E4%B8%8D%E4%BD%BF%E7%94%A8docker%20commit%E5%8E%9F%E5%9B%A0.mp4" width="800" height="480" type="video/mp4">
</video>