---
layout: post
title: flume-example-netcat
tags: example
categories: basicTech
published: true
---

* TOC
{:toc}


## 1 需求简介
这是flume教程上的例子，单节点监听44444端口，传输数据到控制台。<br>
flume的安装教程，参阅[flume安装](https://www.pythonbug.com/basictech/flume-install/)

## 2 需求分析
使用flume，就是写flume的配置文件。<br>
在配置文件中使flume的各个组件能够串接起来。<br>
还需要注意的一点是：选择恰当的组件。<br>
source选择：由于是监控端口，所以选择netcat<br>
channel选择：内存型即可<br>
sink选择：输出到控制台，所以选择logger<br>

## 3 配置文件
>文件名称：singleTest.conf
>文件内容：

~~~shell
# singleTest.conf: A single-node Flume configuration

# Name the components on this agent
a1.sources = p_source1
a1.sinks = p_sink1
a1.channels = p_channel1

# Describe/configure the source
a1.sources.p_source1.type = netcat
a1.sources.p_source1.bind = 192.168.31.2
a1.sources.p_source1.port = 44444

# Describe the sink
a1.sinks.p_sink1.type = logger

# Use a channel which buffers events in memory
a1.channels.p_channel1.type = memory

# Bind the source and sink to the channel
a1.sources.p_source1.channels = p_channel1
a1.sinks.p_sink1.channel = p_channel1
~~~

## 4 启动agent
~~~shell
flume-ng agent --conf $FLUME_HOME/conf \
--conf-file /home/pythonbug/code/Learn/flume/singleTest.conf \
--name a1 -Dflume.root.logger=INFO,console
~~~

## 5 疑问
这里的 `--conf`是global options，我以为是singleTest.conf文件所在的目录。经过实验，发现不是，而是应该为flume安装目录下面的conf目录。