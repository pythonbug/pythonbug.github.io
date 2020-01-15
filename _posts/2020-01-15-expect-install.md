---
layout: post
title: EXPECT-INSTALL
tags: install
categories: basicTech
published: true
---

* TOC
{:toc}

# 1、 解压

~~~shell
tar -zxf expect5.45.tar.gz
tar -zxf tcl8.4.11-src.tar.gz 
~~~

# 2、编译&安装tcl
~~~shell
./configure --prefix=/usr/tcl --enable-shared
sudo make && sudo make install
~~~

# 3、复制文件tclUnixPort.h
~~~shell
cd ..
cp unix/tclUnixPort.h generic/
~~~

# 4、开始安装expect
~~~shell
cd expect5.45/
./configure --prefix=/usr/expect --with-tcl=/usr/tcl/lib --with-tclinclude=../tcl8.4.11/generic
sudo make && sudo make install
~~~

# 5、添加软链接
~~~shell
sudo ln -s /usr/tcl/bin/expect /usr/bin/expect
~~~