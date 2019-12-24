---
layout: post
title:  "Debian Buster10安装"
date:   2019-12-11 13:33
categories: Debian Linux
tags: 安装
excerpt: 知识点记录
author: Pythonbug
mathjax: true
---
## 1 由于万恶之墙的存在，所以需要更新一下apt源
```
# root用户
# 先备份一下
cp /etc/apt/sources.list /etc/apt/sources.listbk
# 设置国内的源
# 根据自己的版本去选择
# 阿里
https://developer.aliyun.com/mirror
# 清华
https://mirror.tuna.tsinghua.edu.cn/help/debian/
```
## 2 我的是Debian10 Buster 选择清华的
### 2.1 好像需要把https换成htpp，不然更新apt-get update的时候会报错什么验证
```
# root用户
vi /etc/apt/sources.list
```
### 2.2 将原有的注释，添加如下内容
```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-updates main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-updates main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-backports main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-backports main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian-security buster/updates main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security buster/updates main contrib non-free
```
## 3 更新软件源
```
apt-get update
```
## 4 安装ssh
```
apt-get install ssh
```
## 5 安装sudo
```
apt-get install sudo -y
```
### 5.1 将本地用户添加到sudo用户组
```
su - root
第一种方法，直接编辑/etc/sudoers文件
xxxx   ALL=(ALL:ALL) ALL
第二种方法，usermod -aG sudo xxxxx
使用第二种方法之后，需要重新登陆一下
```
## 6 安装vim
```
apt-get install vim
```
## 7 安装防火墙
```
sudo apt install ufw
```
### 7.1 设置一下安全策略
```
sudo ufw default deny incoming
sudo ufw default allow outgoning
sudo ufw allow ssh
```
### 7.2 开启某个端口
```
开启80端口
sudo ufw allow 80
```
### 7.3 删除某个规则
```
sudo ufw status numbered
sudo ufw delete number
```