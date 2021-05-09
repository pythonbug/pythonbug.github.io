---
layout: post
title: mount command
tags: install
categories: basicTech
published: true
---

* TOC
{:toc}


>展示磁盘信息，包括没有挂载的

- `sudo fdisk -l`

>格式化磁盘

- `sudo mkfs.ext4 /dev/sda1`

>挂载磁盘

- `sudo mount -t ext4 /dev/sda1 /home/pi/data`

