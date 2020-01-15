---
layout: post
title: EXPECT-INSTALL
tags: install
categories: basicTech
published: true
---

* TOC
{:toc}

# 1、 下载expect5.45.tar.gz、tcl8.4.11-src.tar.gz解压

~~~shell
tar -zxf expect5.45.tar.gz
tar -zxf tcl8.4.11-src.tar.gz 
~~~

~~~shell
# 编译&安装
./configure --prefix=/usr/tcl --enable-shared
sudo make && sudo make install
~~~

~~~shell
# 复制文件tclUnixPort.h
cd ..
cp unix/tclUnixPort.h generic/
~~~

~~~shell
# 开始安装expect
cd expect5.45/
./configure --prefix=/usr/expect --with-tcl=/usr/tcl/lib --with-tclinclude=../tcl8.4.11/generic
sudo make && sudo make install
sudo ln -s /usr/tcl/bin/expect /usr/bin/expect
~~~