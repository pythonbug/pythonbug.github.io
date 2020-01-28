---
layout: post1
title: flume-example-exec
tags: example
categories: basicTech
---

* TOC
{:toc}


## 1 需求简介
监控一个文件，实时采集新增的数据输出到控制台。<br>
flume的安装教程，参阅[flume安装](https://www.pythonbug.com/basictech/flume-install/)


## 2 需求分析
source: 获取文件的新内容，使用命令行获取文件新增内容 `tail -f `，所以source选用 exec-source，由于exec-source具有一定风险，替换成taildir source<br>
channel: 内存型
sink: 输出到控制台，还是选择logger

## 3 配置文件
>文件名称：singleTestExec.conf
>文件内容：

~~~shell
# singleTestExec.conf: A single-node Flume configuration
  
# Name the components on this agent
a1.sources = p_source1
a1.sinks = p_sink1
a1.channels = p_channel1

# Describe/configure the source
a1.sources.p_source1.type = TAILDIR
a1.sources.p_source1.filegroups = f1
a1.sources.p_source1.filegroups.f1 = /home/pythonbug/testfile

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
--conf-file /home/pythonbug/code/Learn/flume/singleTestExec.conf \
--name a1 -Dflume.root.logger=INFO,console
~~~