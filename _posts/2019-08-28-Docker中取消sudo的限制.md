---
layout: post
title:  "Docker中取消sudo的限制"
date:   2019-08-28 18:52
categories: Docker
tags: sudo Docker
excerpt: 随笔记录
author: Pythonbug
mathjax: true
---

## 1、添加docker组
```
sudo groupadd docker
```
![将pythonbug用户添加到docker组](https://github.com/pythonbug/myPictures/blob/master/Debian%E4%B8%AD%E6%B7%BB%E5%8A%A0%E7%94%A8%E6%88%B7.png?raw=true)
## 2、将当前用户加入到docker组里面
```
## 我当前用户是pythonbug
sudo vim /etc/group
```

## 3、重启docker的进程
```
sudo service docker restart
```

## 4、重新登陆linux
![](https://github.com/pythonbug/myPictures/blob/master/QQ%E6%88%AA%E5%9B%BE20190828195354.png?raw=true)