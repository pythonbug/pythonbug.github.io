---
layout: post
title:  "Debian10中设置DNS"
date:   2019-09-08 22:35
categories: Linux
tags: Debian 网络 DNS
excerpt: 知识点记录
author: Pythonbug
mathjax: true
---

## 谷歌出来的解决办法
没有DNS还是很麻烦的，配置的apt源就没法使用。因为无法解析网址。
在Debian 10 Buster中。我也查阅了一些外网教程，其中有一个是在/etc/network/interfaces文件中，添加
```
dns-nameservers 8.8.8.8
```
我自己试了一下没什么卵用。不知道怎么回事。你们可以自己试一下。

## 我自己的解决办法
直接vi /etc/resolv.conf
然后添加
```
nameserver 8.8.8.8
```
就搞定了。