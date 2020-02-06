---
layout: post
title: zk-install
tags: note
categories: linux
published: true
---

* TOC
{:toc}


## 1 问题描述
创建的Java Producer API发送数据，但是consumer的时候却无法看到发送的数据。不过可以成功创建topic。

## 2 机器简介
我有四台linux集群（不是虚拟机，都是单独的物理机，四台树莓派）：

| hostname | broker-list      |IP地址|
|:--------:| :-------------:|:-------------:|
| power1 | broker0 |192.168.31.2|
| slaves1 | broker1 |192.168.31.3|
| slaves2 | broker2 |192.168.31.4|
| slaves3 | broker3 |192.168.31.5|

## 3 本地代码
我是在自己笔记本（windows）上开发的代码，然后直接运行了Idea。

~~~java
import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.Producer;
import org.apache.kafka.clients.producer.ProducerRecord;

import java.util.Properties;

public class KafkaProducer2 {
    public static void main(String[] args) {
        Properties props = new Properties();
        props.put("bootstrap.servers", "power1:9092");
        props.put("acks", "0");
        props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
        props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

        Producer<String, String> producer = new KafkaProducer<String, String>(props);
        for (int i = 0; i < 100; i++) {
            System.out.println(i);
            //producer.send(new ProducerRecord<String, String>("topic0", Integer.toString(i), Integer.toString(i)));
            ProducerRecord<String, String> records = new ProducerRecord<String,String>("topic0", Integer.toString(i), Integer.toString(i));
        }
        producer.close();
    }
}
~~~

**运行之后，没有报错。且能创建topic。另外，我也在windows的hosts文件中加入了power1**

host文件添加如下：<br>
>power1 192.168.31.2

## 4 解决过程
#### 4.1 添加代码，获取发送之后的信息

>producer.send(records).get();

#### 4.2 新代码如下：

~~~java
import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.Producer;
import org.apache.kafka.clients.producer.ProducerRecord;

import java.util.Properties;
import java.util.concurrent.ExecutionException;

public class KafkaProducer2 {
    public static void main(String[] args) {
        Properties props = new Properties();
        props.put("bootstrap.servers", "power1:9092");
        props.put("acks", "0");
        props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
        props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

        Producer<String, String> producer = new KafkaProducer<String, String>(props);
        for (int i = 0; i < 100; i++) {
            System.out.println(i);
            //producer.send(new ProducerRecord<String, String>("topic0", Integer.toString(i), Integer.toString(i)));
            ProducerRecord<String, String> records = new ProducerRecord<String,String>("topic0", Integer.toString(i), Integer.toString(i));

            // 以下为新增内容：
            try {
                producer.send(records).get();
            } catch (InterruptedException e) {
                e.printStackTrace();
            } catch (ExecutionException e) {
                e.printStackTrace();
            }

        }
        producer.close();
    }
}
~~~

#### 4.3 获取报错如下：
*Caused by: org.apache.kafka.common.errors.TimeoutException: Topic topic0 not present in metadata after 60000 ms.*

#### 4.4 看来还是网络的问题：
修改所有broker的server.properties文件，把所有hostname修改成ip地址

如：
listeners=PLAINTEXT://power1:9092 ----> listeners=PLAINTEXT://192.168.31.2:9092

#### 4.5 再次测试
修改完每一台的server.properties之后重启kafka。运行，解决。

#### 4.6 问题深究
难道说，必须只能用ip地址吗？我相信kafka不会这么不成熟。我只要配置了hostname的解析，那么就应该是正常的。而且没修改之前，我在控制台上produce数据也是可以正常消费的啊。

因此，我怀疑，应该是我的笔记本和这些集群之间的网络问题，并不是server.properties必须使用ip地址。

#### 4.7 证明自己猜想
首先，将power1的server.properties还原成`listeners=PLAINTEXT://power1:9092`
重启kafka，运行java上的producer。正常。

将slaves1的server.properties还原成`listeners=PLAINTEXT://slaves1:9092`
重启kafka，运行java上的producer。正常。

将slaves2的server.properties还原成`listeners=PLAINTEXT://slaves2:9092`
重启kafka，运行java上的producer。正常。

将slaves3的server.properties还原成`listeners=PLAINTEXT://slaves3:9092`
重启kafka，运行java上的producer。**不正常**。

终于找到了问题，slaves3！

#### 4.8 为什么是slaves3
为什么是slaves3，难道说...？

`./kafka-topics.sh --describe --bootstrap-server power1:9092 --topic topic0`

输出：
Topic: topic0   Partition: 0    Leader: 3       Replicas: 3     Isr: 3

原来如此，数据都是在broker3上存着，也就是slaves3这台机器上。

所以，我变更power1,slaves1,slaves2的server.properties都不会影响。

虽然，java代码中写了`props.put("bootstrap.servers", "power1:9092");`，但是实际数据是发送到slaves3上的，而我笔记本上的hosts文件并没有添加slaves3的解析，因此将slaves3的server.properties文件修改成ip就没问题了。

为了统一，我将笔记本上的hosts文件添加所有集群的解析。

192.168.31.2    power1<br>
192.168.31.3    slaves1<br>
192.168.31.4    slaves2<br>
192.168.31.5    slaves3<br>

将所有机器上的server.properties全部换成hostname，就是不用ip。

测试-->成功！