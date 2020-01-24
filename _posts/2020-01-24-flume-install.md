---
layout: post
title: flume-install
tags: install
categories: basicTech
---

* TOC
{:toc}


## 1 简介：
Flume是一个日志采集工具，非常灵活。

## 2 安装前提：
- Java环境，jdk1.8以上
- 充足的内存
- 充足的磁盘空间
- 可读/可写的目录权限

## 3 安装步骤：
#### 3.1 jdk
[jdk1.8的安装](https://www.pythonbug.com/basictech/jdk1.8-install/)

#### 3.2 flume安装
- [下载flume-1.9.0](http://mirror.bit.edu.cn/apache/flume/1.9.0/apache-flume-1.9.0-bin.tar.gz)

~~~shell
# 解压
shell> tar -zxf apache-flume-1.9.0-bin.tar.gz -C ~/app/

# 配置环境变量
export FLUME_HOME=/home/pythonbug/app/apache-flume-1.9.0-bin
export PATH=$FLUME_HOME/bin:$PATH

# 环境变量生效
shell> source ~/.profile
~~~
