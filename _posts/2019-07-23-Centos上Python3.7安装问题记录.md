---
layout: post
title:  "Centos7安装Python3.7"
date:   2019-07-23 18:10
categories: Linux
tags: 虚拟机 Python 安装
author: Pythonbug
excerpt: 安装虚拟机记录。
mathjax: true
---

## 1 zlib not available
下载安装zlib包
[zlib-1.2.11.tar.gz](https://pan.baidu.com/s/1c_0EOdqyNwjEsPn4HTBpPQ)
```sh
tar -zxf zlib-1.2.11.tar.gz
cd zlib-1.2.11
./configure
make && make install
```

## 2 No module named '_ctypes'
```sh
sudo apt-get install libffi-dev
or 
yum install libffi-devel
# 具体的原因未深究，离线安装的方法也未深究
# 先记录下来
```

## 3 import ssl报错 No Module named _ssl
```sh
yum install openssl-devel
```