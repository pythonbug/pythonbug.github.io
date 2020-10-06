---
layout: post
title: JDBC的简单入门
tags: 数据库
categories: 基本概念
published: true
---

* TOC
{:toc}

JDBC操作数据库，我们可以分为以下八个步骤

&nbsp;
## 1 导入数据库驱动包
    JDBC是一种规范，一种接口。
    真正起作用的是各个数据库的实现类。
    所以，我们需要先导入数据库的驱动包。
    我们这里用的是MySQL数据库，因此导入MySQL驱动包。

&nbsp;
## 2 注册驱动
```java
Class.forName("com.mysql.jdbc.Driver")
```

&nbsp;
#### 2.1 为啥要注册驱动
    明确我要操作的是哪一种数据库。
    告诉JDBC，我要使用哪一个数据库的驱动类来实现它。

&nbsp;
#### 2.2 为啥这里一句话就完成了注册驱动
    Class.forName("com.mysql.jdbc.Driver")，把类的字节码加载进内存。
    然后就能注册驱动了吗？说明这个类被加载的时候执行了一段代码。
    我们联想到 ---> 静态代码 ---> 查看com.mysql.jdbc.Driver的源码进行验证。
```java
//
    // Register ourselves with the DriverManager
    //
    static {
        try {
            java.sql.DriverManager.registerDriver(new Driver());
        } catch (SQLException E) {
            throw new RuntimeException("Can't register driver!");
        }
    }
```
果然是这样的，调用了DriverManager类的registerDriver方法。

&nbsp;
#### 2.3 小小的注意点
    在MySQL的5版本之后，这里的Class.forName("com.mysql.jdbc.Driver")可以不用再写。
    因为 MySQL驱动包里面的 META-INF/services/java.sql.Driver文件已经加上了。

&nbsp;
## 3 创建数据库连接对象
```java
Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/learn", "ai88", "5201314");
```

&nbsp;
## 4 准备sql
```java
String sql = "update student set sex='男' where 1=1 and id=903";
```

&nbsp;
## 5 创建执行sql的Statement对象
```java
Statement stmt = connection.createStatement();
```

&nbsp;
## 6 执行sql
```java
int result = stmt.executeUpdate(sql);
```

&nbsp;
## 7 处理结果
```java
System.out.println(result);
```

&nbsp;
## 8 释放资源
```java
stmt.close();
connection.close();
```

&nbsp;
## 9 完整的代码
```java
package org.ai88;

import org.apache.log4j.Logger;

import java.sql.*;

public class Test1 {
    private static Logger logger = Logger.getLogger(Test1.class);

    public static void main(String[] args) throws Exception{
        // 1 导入驱动包 maven中做的
        // 2 注册驱动
        Class.forName("com.mysql.jdbc.Driver");

        // 3 获得数据库连接对象 Connection
        Connection connection = DriverManager.getConnection("jdbc:mysql://192.168.66.203:3306/learn", "ai88", "5201314");

        // 4 定义sql语句
        String sql = "update student set sex='男' where 1=1 and id=903";

        // 5 获得执行sql的statement对象
        Statement stmt = connection.createStatement();

        // 6 执行sql获取结果
        int result = stmt.executeUpdate(sql);
        
        // 7 处理结果
        System.out.println(result);

        // 8 释放资源
        stmt.close();
        connection.close();
    }
}
```
