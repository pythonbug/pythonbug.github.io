---
layout: post
title: SBT-INSTALL
tags: install
categories: basicTech
published: true
---

* TOC
{:toc}

>说明，[in]表示输入，[out]表示命令行输出

## 1 下载

>注意这里的版本是1.3.6
[官网下载sbt](https://piccolo.link/sbt-1.3.6.tgz)

## 2 安装

~~~shell
# 创建一个专门放置这些软件的目录
[in]shell> mkdir ~/app
# 解压至该目录
[in]shell> tar -zxf sbt-1.3.6.tgz -C ~/app/
# 进入该目录
[in]shell> cd ~/app/sbt
~~~

## 3 查看查看当前目录

~~~shell
[in]shell> pwd
[out]shell> /home/pythonbug/app/sbt
~~~

## 4 配置环境变量文件

>我都是Debian系统，环境变量文件是.profile，centos是.bash_profile

~~~shell
[in]shell> vim ~/.profile
~~~

#### 4.1 添加如下内容

~~~shell
// 添加下面内容。注意，你的主目录跟我是不一样的，注意修改
export SBT_HOME=/home/pythonbug/app/sbt
export PATH=$SBT_HOME/bin:$PATH
~~~

#### 4.2 保存退出
`:wq`

#### 4.3 使刚刚配置的环境变量生效
~~~shell
[in]shell> source ~/.profile
~~~
