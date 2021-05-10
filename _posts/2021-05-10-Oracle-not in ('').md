---
layout: post
title: Oracle中的not in ('')
tags: 知识盲点
categories: Oracle数据库
published: true
---

* TOC 
{:toc}
  
### 简要说明
```sql
select * from xxxx where 1=1 and 字段 not in ('');
```

这种写法在Oracle中无法返回任何值。

若要实现相同的功能，应该写成:

```sql
select * from xxxx where 1=1 and 字段 is not null;
```

### 记忆中这样写可行的情况

在一些代码里面，我们需要拼接字符串，可能就会形成 `('a','b',''')` 这种形式。

在最后会有一个`''`形成。

这样怎么可以呢？

原来是这种写法中在 `in` 中而不是 `not in` 中。

例如:

```sql
select * from xxx where 1=1 and 字段 in ('a','b','c','')
```

这种写法是可以查出来表中a,b,c的值的。

另外，在MySQL中，查空字符串就是用的`not in ('')` 这种写法。