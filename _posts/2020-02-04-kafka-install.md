---
layout: post
title: useradd
tags: note
categories: linux
published: true
---

* TOC
{:toc}

>三台树莓派+一台主机安装kafka
# 1 主机先安装
## 1.1 下载
[kafka_2.13-2.4.0](http://mirrors.tuna.tsinghua.edu.cn/apache/kafka/2.4.0/kafka_2.13-2.4.0.tgz)

## 1.2 安装
切换到安装目录：`tar -zxf kafka_2.13-2.4.0.tgz -C ~/app`

## 1.3 设置环境变量
~~~shell
vim ~/.profile

export KAFKA_HOME=/home/pythonbug/app/kafka_2.11-2.2.1
export PATH=$KAFKA_HOME/bin:$PATH

source ~/.profile
~~~

## 1.4 修改配置文件
~~~shell
cd $KAFKA_HOME/config

vim server.properties

~~~
需要关注的几个值：
- broker.id=0
- listeners=PLAINTEXT://power1:9092 (我把主机的hostname换成了power1，详情参照[Linux设置Hostname](https://www.pythonbug.com/basictech/debian-set-hostname/))
- log.dirs=/home/pythonbug/data/kafka-logs
- num.partitions=1
- zookeeper.connect=power1:2181

## 1.5 启动kafka
>启动kafka需要先启动zookeeper，有关kafka的安装启动，参照[zookeeper](https://www.pythonbug.com/linux/zk-install/)
`./kafka-server-start.sh $KAFKA_HOME/config/server.properties`

# 2 树莓派三台安装
>把主机上下载的安装包传输到其中一台树莓派，我的树莓派也设置了hostname，这一台的hostname叫做slaves1。
## 2.1 安装
~~~shell
sftp pythonbug@power1
get kafka_2.13-2.4.0.tgz
tar -zxf kafka_2.13-2.4.0.tgz -C ~/app/
~~~

## 2.2 设置环境变量
~~~shell
vim ~/.profile

export KAFKA_HOME=/home/pi/app/kafka_2.13-2.4.0
export PATH=$KAFKA_HOME/bin:$PATH

source ~/.profile
~~~

## 2.3 分发给其他树莓派机器
另外两台树莓派机器的hostname叫做：slaves2,slaves3
#### 2.3.1 分发kafka
`scp -r kafka_2.13-2.4.0/ pi@slaves2:/home/pi/app`<br>
`scp -r kafka_2.13-2.4.0/ pi@slaves3:/home/pi/app`

#### 2.3.2 分发环境变量
