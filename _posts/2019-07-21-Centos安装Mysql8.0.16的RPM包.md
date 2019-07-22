---
layout: post
title:  "Centos7上的Mysql的安装"
date:   2019-07-21 22:11
categories: Mysql
tags: Mysql Linux
author: Pythonbug
excerpt: 安装记录
mathjax: true
---

* content
{:toc}




## 安装common
```sh
rpm -ivh mysql-community-common-8.0.17-1.el7.x86_64.rpm
```

## 安装libs
```sh
rpm -ivh mysql-community-libs-8.0.17-1.el7.x86_64.rpm
```

## 安装client
```sh
rpm -ivh mysql-community-client-8.0.17-1.el7.x86_64.rpm
```

## 安装server
```sh
rpm -ivh mysql-community-server-8.0.17-1.el7.x86_64.rpm
```

## 初始化数据库
```sh
mysqld --initialize --console
```

## 目录授权
```sh
chown -R mysql:mysql /var/lib/mysql/
```

## 启动mysql的服务
```sh
systemctl start mysqld
# 停止是service mysqld stop
```

## 查看mysql服务状态
```sh
service mysqld status
```

## 查看临时密码，用作第一次登录
```sh
cat /var/log/mysqld.log
```
![](https://github.com/pythonbug/myPictures/blob/master/mysql%E7%9A%84%E7%AC%AC%E4%B8%80%E6%AC%A1%E9%BB%98%E8%AE%A4%E5%AF%86%E7%A0%81.png?raw=true)

## 用临时密码登录数据库
```sh
mysql -uroot -p
# 回车之后输入上面的初始默认密码
```

## 登录成功之后修改密码
```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY '7jq89C9jE=MC^2'
# 这里好像不写localhost直接写ip地址会报错，要先换密码。难道是当成了对远程的机器执行命令？
```

## 设置一下可以远程连接
```sql
update user set host='%' where user='root';
```

## 刷新
```sql
flush privileges;
```

## 查看一下防火墙设置
```sh
firewall-cmd --state
# running ： 运行中，下面的步骤是防火墙运行中的情况
# not running ： 未运行，就不用管了，这样最好
```

## 查看防火墙已经开放的端口
```sh
firewall-cmd --list-ports
# 若3306默认端口未开放，则需要设置开放，否则远程将无法连接
# 若已开发，则不用再管，直接去Navicat等工具去连接使用
```

## 若3306默认端口未开放
```sh
firewall-cmd --zone=public --add-port=3306/tcp --permanet
#–zone #作用域
#–add-port=80/tcp #添加端口，格式为：端口/通讯协议
#–permanent #永久生效，没有此参数重启后失效
```

## 关闭端口的命令
```sh
firewall-cmd --zone=public --remove-port=3306/tcp --permanet
```

## 重启防火墙命令
```sh
firewall-cmd --reload
```

## 附件下载
- [mysql-community-common-8.0.17-1.el7.x86_64](https://pan.baidu.com/s/1CTgRHtW5njNLBfFLvyHR2g)
提取码：89m7

- [mysql-community-server-8.0.17-1.el7.x86_64](https://pan.baidu.com/s/1FjVPcSfaZje92CoKxwOa8Q)
提取码：3aao

- [mysql-community-libs-8.0.17-1.el7.x86_64](https://pan.baidu.com/s/1QxUYzPyQH9oyxjmjnrESfg) 
提取码：qdgb 

- [mysql-community-client-8.0.17-1.el7.x86_64](https://pan.baidu.com/s/1xXTzVmycwpxNbIyKvtZa6A) 
提取码：mq19 

