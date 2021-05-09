---
layout: post
title: class-object-references
tags: note
categories: Java
published: true
---

* TOC
{:toc}


## 1 这三者在代码中具体所指
![类对象及引用.png](https://i.loli.net/2020/02/04/zKoGqZ95ljaQ7iB.png)

## 2 类和对象的关系
- 类是对象的模板，对象是类的一个实例
- 一个Java程序中同一个package下类名必须是独一无二的
    - 因为类名必须和创建这个类名的文件名一致，众所周知：一个目录下面的文件名肯定是不能重复的
- 一个类可以有很多个对象
- 一个对象只能根据一个类来创建
    - 很明显：没有`new Animal() People() Alien()`这种写法

## 3 引用和类以及对象的关系
- 引用必须是且只能是一个类的引用
    - 很明显：没有 `Animal m1 = new Animal() People() Alien()`这种莫名其妙的写法
- 引用只能指向其所属类型的类的对象
    - 很明显：`Animal m1 = new People()`是错误的
- 只能通过指向一个对象的引用，来操作一个对象。比如，访问某个成员变量。