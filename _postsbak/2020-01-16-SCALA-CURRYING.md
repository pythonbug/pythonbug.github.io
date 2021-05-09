---
layout: post
TITLE: SCALA-CURRYING
tags: example
categories: scala
published: true
---

* TOC 
{:toc}


# 前言：
>学习scala的时候，碰到一个新名词，柯里化。不太理解。因此，找了个例子，在此记录一下。

# 例子
~~~scala
scala> def carrie(x:Int)(y:Int) = x+y
scala> val a1 = carrie(1)_
scala> a1(2)
res0: Int = 3
~~~