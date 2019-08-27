---
layout: post
title:  "Debian离线安装Docker"
date:   2019-08-27 21:05
categories: Docker
tags: Docker 离线 安装
excerpt: 总结随笔
author: Pythonbug
mathjax: true
---

## 1、卸载旧版本docker                                                               
```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

## 2、下载deb package
```
# 根据自己的Debian版本去选择
https://download.docker.com/linux/debian/dists/stretch/pool/stable/amd64/
```

## 3、安装
```
# 注意，这个安装之后是自动会启动docker服务的
sudo dpkg -i /path/to/package.deb
# 检验一下
sudo docker run hello-world
```

## 4、附件
[docker的Debian包](https://download.docker.com/linux/debian/dists/stretch/pool/stable/amd64/docker-ce_19.03.1~3-0~debian-stretch_amd64.deb)

## 5、视频