---
layout: post
title: Flink的SQL用法
tags: 新技能点
categories: 大数据
published: true
---

* TOC 
{:toc}
  
- 第一步创建出StreamExecutionEnvironment。
`StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment()`
  
- 第二步先拿到流数据，假设从kafka拿到的数据
`DataStream<String> ds = env.addSource(new FlinkKafkaConsumer(topic,new SimpleStringShcema(),props))`
  
- 第三步从StreamExecutionEnvironment创造出StreamTableEnvironment。
`StreamTableEnvironment tableEnv = StreamTableEnvironment.create(env)`
  
- 第四步tableEnv从流里面拿到Table类型的流
`Table t = tableEnv.fromDataStream(ds)`
  
- 第五步开始TableAPI操作
`Table t2 = t.select(...)...`
  
- 第四步的第二种，利用tableEnv在环境中注册新的视图，这里没有返回值
`tableEnv.createTemporaryView(表或者视图的名字,ds)`
  
- 第五步编写sql，和正常的sql一样写就可以
`String sql = "select xxx from 上述注册的表或者视图的名字 where 1=1 " `
  
- 第六步tableEnv执行sql
`Table t = tableEnv.sqlQuery(sql)`