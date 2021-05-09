---
layout: post
title: Debian-set-Hostname
tags: install
categories: basicTech
published: true
---

* TOC
{:toc}


## 1 简介：
>Debian里面设置hostname，需要修改两个文件：/etc/hosts、/etc/hostname

## 2 /etc/hostname
~~~shell
sudo vim /etc/hostname
xxxxx # 你设置的主机名
~~~

## 3 /etc/hosts
~~~shell
sudo vim /etc/hosts
ip地址   主机名 # 如：192.168.6.8  pythonbug
~~~

## 4 注意一下

写这篇博客之前，我查了点资料，发现有个地方这样写到：
>这里特别提醒大家注意的是，如果在hostname中修改了主机名，一定要在hosts里加入这样的行：
127.0.0.1 localhost 修改的主机名
或者这样
127.0.0.1 修改的主机名
因为在linux里很多命令都会用到gethostbyname()这个函数，如果改了主机名而又没有在hosts里更新，那么这个命令是无法执行的。

我的机器里并没有这样配置，我只是在原先的/etc/hosts文件下方增加了 "3" <br>处的内容。目前还没有遇到这样的问题，可能是我这里直接配置了在局域网的IP和主机名。