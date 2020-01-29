---
layout: post1
title: java-datatype-long
tags: 知识盲点
categories: Java
---

* TOC
{:toc}


## 1 盲点简介
如何理解Java代码中的<br>
~~~java
Long longvalue = 99999999999L;
~~~
这里为什么要加上`L`后缀呢？<br>
一开始，我觉得只需要记住这个就行。但是记住的东西，总会有忘记的时候。<br>
那我们就来理解一下。<br>

## 2 原理解析
因为： 整数的默认数据类型是int<br>
因为： int的值域范围是-2147483648~2147483647<br>
所以： 在表示某些超出这些范围的数字的时候，需要加上其他数据类型。来表明不再使用Java默认整数的数据类型int。<br>
总结： 这就是为什么99999999999为什么加 `L`的原因。<br>

## 3 举一反三
为什么在java中<br>
~~~java
float fvalue = 0.9;
~~~
会报错<br>

在java中，浮点数的默认类型都是double。double的精度要比float高。我们知道，高精度的数据类型是不能直接向低精度数据类型转换的。<br>
所以，这里的0.9，不能直接赋值给成float类型的变量fvalue。<br>
需要写成:<br>
~~~java
float fvalue = 0.9f;
~~~