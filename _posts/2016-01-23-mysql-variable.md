---
layout: post
title:  "MySQL的变量"
date: 2016-01-28 15:28:19
categories: MySQL
tags: MySQL show
---


# 用户变量 #

用户变量与连接有关。也就是说，一个客户端定义的变量不能被其它客户端看到或使用。当客户端退出时，该客户端连接的所有变量将自动释放。

```
SET @var_name = expr [, @var_name = expr] ...
```

```
mysql> SET @t1=0, @t2=1, @t3=3;
Query OK, 0 rows affected (0.00 sec)
```

```
mysql> select @t1, @t2, @t3;
+------+------+------+
| @t1  | @t2  | @t3  |
+------+------+------+
|    0 |    1 |    3 |
+------+------+------+
1 row in set (0.00 sec)
```

```
mysql> select @t1:=@t2+@t3;
+--------------+
| @t1:=@t2+@t3 |
+--------------+
|            4 |
+--------------+
```

# 系统变量 #

- 全局变量：影响服务器整体操作。
- 会话变量：影响具体客户端连接的操作。

服务器启动后，通过连接服务器并执行SET GLOBAL var_name语句，可以动态更改这些全局变量。要想更改全局变量，必须具有SUPER权限。  
对于动态会话变量，客户端可以通过SET SESSION var_name语句更改它们。设置会话变量不需要特殊权限，但客户端只能更改自己的会话变量。


要想设置一个GLOBAL变量的值，使用下面的语法：

```
mysql> SET GLOBAL sort_buffer_size=value;
mysql> SET @@global.sort_buffer_size=value;
```


要想设置一个SESSION变量的值，使用下面的语法：

```
mysql> SET SESSION sort_buffer_size=value;
mysql> SET @@session.sort_buffer_size=value;
mysql> SET sort_buffer_size=value;
```

如果设置变量时不指定GLOBAL、SESSION或者LOCAL，默认使用SESSION。

要想检索一个GLOBAL变量的值，使用下面的语法：

```
mysql> SELECT @@global.sort_buffer_size;
mysql> SHOW GLOBAL VARIABLES like 'sort_buffer_size';
```

要想检索一个SESSION变量的值，使用下面的语法：

```
mysql> SELECT @@sort_buffer_size;
mysql> SELECT @@session.sort_buffer_size;
mysql> SHOW SESSION VARIABLES like 'sort_buffer_size';
```
