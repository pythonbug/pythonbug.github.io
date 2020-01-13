---
layout: post
title: scala type casting
tags: type-casting
categories: Scala
---


* TOC 
{:toc}


# 核心

- 不允许高往低转换，只可以低往高转换。

- 但是注意，低往高转换可能会丢失精度

# 图示

![avatar](https://docs.scala-lang.org/resources/images/tour/type-casting-diagram.svg)

# 示例

~~~scala
val x: Long = 987654321
val y:Float = x //9.8765434E8，这里的精度就丢失了
~~~

~~~scala
val x: Long = 987654321
val y:Int = x //这里就报错了
~~~