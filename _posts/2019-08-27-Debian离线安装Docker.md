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
sudo apt-get remove docker-ce docker docker-engine docker.io containerd runc
```

## 2、下载deb package
```
# 根据自己的Debian版本去选择,我的是buster
https://download.docker.com/linux/debian/dists/buster/pool/stable/amd64/
# 下载containerd.io
# 下载docker-ce-cli
# 下载docker-ce
尽量版本都选择同一个版本或者都为最新的，否则安装的时候会报错。
```

## 3、安装
```
# 注意，这个安装之后是自动会启动docker服务的
sudo dpkg -i /path/to/package.deb

# 安装containerd.io
sudo dpkg -i containerd.io_1.2.6-3_amd64.deb

# 安装docker-ce-cli
sudo dpkg -i docker-ce-cli_19.03.2_3-0_debian-buster_amd64.deb

# 安装docker-ce
sudo dpkg -i docker-ce_19.03.2_3-0_debian-buster_amd64.deb

# 检验一下
sudo docker run hello-world
```

## 4、附件
[docker-ce](https://download.docker.com/linux/debian/dists/buster/pool/stable/amd64/docker-ce_18.09.9~3-0~debian-buster_amd64.deb)

[docker-ce-cli](https://download.docker.com/linux/debian/dists/buster/pool/stable/amd64/docker-ce-cli_18.09.9~3-0~debian-buster_amd64.deb)

[containerd.io](https://download.docker.com/linux/debian/dists/buster/pool/stable/amd64/containerd.io_1.2.6-3_amd64.deb)