---
layout: post
title: zk-install
tags: note
categories: linux
published: true
---

* TOC
{:toc}


## 1 下载
[zookeeper3.5.6下载](http://archive.apache.org/dist/zookeeper/zookeeper-3.5.6/apache-zookeeper-3.5.6-bin.tar.gz)

## 2 安装
切换到安装目录：`tar -zxf apache-zookeeper-3.5.6-bin.tar.gz -C ~/app`

## 3 修改conf文件
切换到配置文件目录：`cd ~/app/apache-zookeeper-3.5.6-bin/cof/`

修改文件：
~~~shell
cp zoo_sample.cfg zoo.cfg

vim zoo.cfg

dataDir=/home/pythonbug/data/zookeeper
~~~

## 4 添加环境变量
~~~shell
vim ~/.profile

export ZK_HOME=/home/pythonbug/app/apache-zookeeper-3.5.6-bin
export PATH=$ZK_HOME/bin:$PATH

source ~/.profile
~~~

## 5 运行zookeeper
`$ZK_HOME/bin/zkServer.sh start`

## 6 检查一下
`jps`

看是否出现：QuorumPeerMain