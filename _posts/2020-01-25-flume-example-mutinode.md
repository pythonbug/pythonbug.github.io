---
layout: post1
title: flume-example-mutinode
tags: example
categories: basicTech
---

* TOC
{:toc}


## 1 需求简介
监控B机器上的数据文件，将新增数据传输到A机器上。<br>
flume的安装教程，参阅[flume安装](https://www.pythonbug.com/basictech/flume-install/)<br>
扩展：监控C、D机器上的文件，与B一起将数据发送到A上面。

## 2 需求分析
#### 2.1 机器A：
- source: avro source
- sink: logger sink
- channel: memory

#### 2.2 机器B:
- source: taildir source
- sink: avro sink
- channel: memory

#### 2.3 机器C:
- source: taildir source
- sink: avro sink
- channel: memory

#### 2.4 机器D:
- source: taildir source
- sink: avro sink
- channel: memory

## 3 配置文件
#### 3.1 A机器上的配置文件

>文件名称：Anode.conf
>文件内容：

~~~shell
# Anode.conf: A single-node Flume configuration
  
# Name the components on this agent
a1.sources = p_source1
a1.sinks = p_sink1
a1.channels = p_channel1

# Describe/configure the source
a1.sources.p_source1.type = avro
a1.sources.p_source1.bind = power1
a1.sources.p_source1.port = 44444

# Describe the sink
a1.sinks.p_sink1.type = logger

# Use a channel which buffers events in memory
a1.channels.p_channel1.type = memory

# Bind the source and sink to the channel
a1.sources.p_source1.channels = p_channel1
a1.sinks.p_sink1.channel = p_channel1
~~~

#### 3.2 B/C/D机器上的配置文件
>文件名称：datanode.conf
>文件内容：

~~~shell
# datanode.conf: A single-node Flume configuration
  
# Name the components on this agent
a1.sources = p_source1
a1.sinks = p_sink1
a1.channels = p_channel1

# Describe/configure the source
a1.sources.p_source1.type = TAILDIR
a1.sources.p_source1.filegroups = f1
a1.sources.p_source1.filegroups.f1 = /home/pi/testfile

# Describe the sink
a1.sinks.p_sink1.type = avro
a1.sinks.p_sink1.hostname = power1
a1.sinks.p_sink1.port = 44444

# Use a channel which buffers events in memory
a1.channels.p_channel1.type = memory

# Bind the source and sink to the channel
a1.sources.p_source1.channels = p_channel1
a1.sinks.p_sink1.channel = p_channel1
~~~

## 4 启动
#### 4.1 启动A服务器
>先执行监听服务器 

~~~shell
flume-ng agent --conf $FLUME_HOME/conf \
--conf-file /home/pythonbug/code/Learn/flume/Anode.conf \
--name a1 -Dflume.root.logger=INFO,console
~~~

### 4.2 启动B/C/D服务器
~~~shell
flume-ng agent --conf $FLUME_HOME/conf \
--conf-file /home/pi/datanode.conf \
--name a1
~~~

## 5 注意
**logger sink的输出有点问题：只能输出16字节大小，并且就算设置了logger-sink的maxBytesToLog属性也没有啥效果**