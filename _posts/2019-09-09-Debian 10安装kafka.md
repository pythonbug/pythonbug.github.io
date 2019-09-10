---
layout: post
title:  "Debian 10部署安装单节点单broker"
date:   2019-09-09 22:23
categories: Kafka
tags: Kafka 安装
excerpt: 错误知识点记录
author: Pythonbug
mathjax: true
---

## Step 1: 确定Java环境
```
java -version
```
如果报错了呢，就去下载一个适合的版本JDK安装一下吧。


#### Step 1.1: 下载
这里提供了一个百度网盘的地址：
[jdk1.8 Linux 64](https://pan.baidu.com/s/1EOcJBbrLSsp-K2opJzVKRg)

#### Step 1.2: 解压
```
tar -zxf jdk-8u221-linux-x64.tar.gz
```

#### Step 1.3: 设置环境变量
```
mkdir ~/jdk
mv jdk1.8.0_221 ~/jdk
vim ~/.profile
## 添加如下内容
export JAVA_HOME=$HOME/jdk/jdk1.8.0_221
export PATH=$PATH:$JAVA_HOME/bin
```

#### Step 1.4: 生效一下
```
source ~/.profile
```

#### Step 1.5: 再次测试一下
```
java -version
```

## Step 2: Zookeeper安装

#### Step 2.1: 下载
[Zookeeper-3.4.5-cdh5.7.0](https://pan.baidu.com/s/1VDnSVI3GAe9-s_ZRotTJ3A)

#### Step 2.2: 解压配置环境变量
```
vim ~/.profile
## 添加如下内容
export ZK_HOME=$HOME/zookeeper-3.4.5-cdh5.7.0
export PATH=$PATH:$ZK_HOME/bin
```

#### Step 2.3: 生效一下
```
source ~/.profile
```

#### Step 2.4: 配置一下数据存储目录
```
mkdir ~/zk_data
cd zookeeper-3.4.5-cdh5.7.0/conf
cp zoo_sample.cfg zoo.cfg
vim zoo.cfg
## 修改一下dataDir
dataDir=/home/pythonbug/zk_data
```

#### Step 2.5: 启动
```
## 由于我们配置了环境变量，所以直接启动，不需要再进入到zookeeper的目录下面了
zkServer.sh start
zkCli.sh
```

## Step 3: Kafka安装
#### Step 3.1: 下载
[kafka_2.11-0.9.0.0](https://pan.baidu.com/s/1LbPRXIDqyIc72dERlsZQtQ)

#### Step 3.2: 解压配置环境变量
```
tar -zxf kafka_2.11-0.9.0.0.tgz
vim ~/.profile
## 添加如下内容
export KAFKA_HOME=$HOME/kafka_2.11-0.9.0.0
export PATH=$PATH:$KAFKA_HOME/bin
```

#### Step 3.3: 生效一下
```
source ~/.profile
```

#### Step 3.4: 设置一下Kafka的配置文件
```
cd kafka_2.11-0.9.0.0/config
vim server.properties
## 修改如下设置
host.name=Server，如果不知道的话，执行一下`hostname`命令，我的名字是Server

log.dirs=/home/pythonbug/kafka-logs 自己创建一个目录，在/tmp目录下重启之后就会自动清空日志。

zookeeper.connect=Server:2181 这里也把localhost修改一下，由于我的zookeeper也装在了Server上所以这里也是Server
```

#### Step 3.5: 启动Kafka
```
kafka-server-start.sh $KAFKA_HOME/config/server.properties
```

#### Step 3.6: 测试一下

###### Step 3.6.1: 创建一个topic，名字是test
```
kafka-topics.sh --create --zookeeper Server:2181 --replication-factor 1 --partitions 1 --topic test
```

###### Step 3.6.2: 查看topic
```
kafka-topics.sh --list --zookeeper Server:2181
```

###### Step 3.6.3: 生产消息
```
# 这边我用Server的这个hostname就报错，DNS无法解析。换成localhost或者直接ip地址就没问题了，不知道你们是否报错，可以都试试。
kafka-console-producer.sh --broker-list localhost:9092 --topic test
```

###### Step 3.6.4: 接收消息（也就是所谓的消费消息）
```
kafka-console-consumer.sh --zookeeper Server:2181 --topic test --from-beginning
## from-beginning表示从第一条生产出来的消息开始消费。不加的话就是当前接收消息启动时候最新的一条开始算
```