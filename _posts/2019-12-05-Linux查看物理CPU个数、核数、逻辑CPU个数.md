---
layout: post
title:  "Linux查看物理CPU个数"
date:   2019-12-05 21:33
categories: Linux
tags: Linux 原理
excerpt: 知识点记录
author: Pythonbug
mathjax: true
---

### 1 总核数
总核数 = 物理CPU个数 * 每个物理CPU核心数

### 2 总逻辑CPU数
总逻辑CPU数 = 物理CPU个数 * 每个物理CPU核心数 * 超线程数

### 3 查看物理CPU个数
```
cat /proc/cpuinfo | grep "physical id"|sort|uniq|wc -l
```

### 4 查看每个CPU的核心数
```
cat /proc/cpuinfo | grep "core id"| sort|uniq|wc -l
```

### 5 查看逻辑CPU个数
```
cat /proc/cpuinfo |grep "processor"|wc -l
```

### 6 查看CPU的信息
```
lscpu
```