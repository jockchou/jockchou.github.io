---
layout: post
title:  "MySQL的show命令语法"
date: 2016-01-28 11:15:49
categories: MySQL
tags: MySQL show
---

SHOW命令有许多种格式，用来查看数据库，表，列和服务器状态信息。 SHOW命令后面可以带 LIKE 用于匹配，有的SHOW后面还可以跟WHERE条件。

show命令的官方手册：
http://dev.mysql.com/doc/refman/5.7/en/show.html

# 命令集合 #

```
mysql> ? show
Name: 'SHOW'
Description:
SHOW has many forms that provide information about databases, tables,
columns, or status information about the server. This section describes
those following:

SHOW {BINARY | MASTER} LOGS
SHOW BINLOG EVENTS [IN 'log_name'] [FROM pos] [LIMIT [offset,] row_count]
SHOW CHARACTER SET [like_or_where]
SHOW COLLATION [like_or_where]
SHOW [FULL] COLUMNS FROM tbl_name [FROM db_name] [like_or_where]
SHOW CREATE DATABASE db_name
SHOW CREATE EVENT event_name
SHOW CREATE FUNCTION func_name
SHOW CREATE PROCEDURE proc_name
SHOW CREATE TABLE tbl_name
SHOW CREATE TRIGGER trigger_name
SHOW CREATE VIEW view_name
SHOW DATABASES [like_or_where]
SHOW ENGINE engine_name {STATUS | MUTEX}
SHOW [STORAGE] ENGINES
SHOW ERRORS [LIMIT [offset,] row_count]
SHOW EVENTS
SHOW FUNCTION CODE func_name
SHOW FUNCTION STATUS [like_or_where]
SHOW GRANTS FOR user
SHOW INDEX FROM tbl_name [FROM db_name]
SHOW MASTER STATUS
SHOW OPEN TABLES [FROM db_name] [like_or_where]
SHOW PLUGINS
SHOW PROCEDURE CODE proc_name
SHOW PROCEDURE STATUS [like_or_where]
SHOW PRIVILEGES
SHOW [FULL] PROCESSLIST
SHOW PROFILE [types] [FOR QUERY n] [OFFSET n] [LIMIT n]
SHOW PROFILES
SHOW SLAVE HOSTS
SHOW SLAVE STATUS [NONBLOCKING]
SHOW [GLOBAL | SESSION] STATUS [like_or_where]
SHOW TABLE STATUS [FROM db_name] [like_or_where]
SHOW [FULL] TABLES [FROM db_name] [like_or_where]
SHOW TRIGGERS [FROM db_name] [like_or_where]
SHOW [GLOBAL | SESSION] VARIABLES [like_or_where]
SHOW WARNINGS [LIMIT [offset,] row_count]

like_or_where:
    LIKE 'pattern'
  | WHERE expr

If the syntax for a given SHOW statement includes a LIKE 'pattern'
part, 'pattern' is a string that can contain the SQL "%" and "_"
wildcard characters. The pattern is useful for restricting statement
output to matching values.

Several SHOW statements also accept a WHERE clause that provides more
flexibility in specifying which rows to display. See
http://dev.mysql.com/doc/refman/5.7/en/extended-show.html.

URL: http://dev.mysql.com/doc/refman/5.7/en/show.html
```

# 归纳 #


表相关的：

```
SHOW INDEX FROM tbl_name [FROM db_name]
SHOW [FULL] COLUMNS FROM tbl_name [FROM db_name] [like_or_where]
SHOW TABLE STATUS [FROM db_name] [like_or_where]
```

查看用户的权限：

```
SHOW GRANTS FOR root;
```

查看表的列信息：

```
SHOW COLUMNS FROM user;
```

查看表的索引：

```
SHOW INDEX FROM user;
```

查看表的状态：

```
mysql> SHOW TABLE STATUS FROM mysql WHERE Name='user'\G;
*************************** 1. row ***************************
           Name: user
         Engine: MyISAM
        Version: 10
     Row_format: Dynamic
           Rows: 3
 Avg_row_length: 122
    Data_length: 368
Max_data_length: 281474976710655
   Index_length: 4096
      Data_free: 0
 Auto_increment: NULL
    Create_time: 2015-12-23 19:28:52
    Update_time: 2016-01-28 10:56:07
     Check_time: NULL
      Collation: utf8_bin
       Checksum: NULL
 Create_options: 
        Comment: Users and global privileges
1 row in set (0.00 sec)
```


查看系统支持的字符集：

```
SHOW CHARACTER SET
```

查看系统支持的权限：

```
SHOW PRIVILEGES;
```

查看系统所有的引擎：

```
SHOW ENGINES;
```

SHOW PROCESSLIST命令：
用来展示所有正在运行中的处理线程，这些信息也可以在INFORMATION_SCHEMA的PROCESSLIST表中查到。如果拥有 PROCESS 权限，可以查看所有的线程，否则只能查看自己的线程。

```
SHOW [FULL] PROCESSLIST;
```

SHOW [FULL] PROCESSLIST不能查看后台线程的状态，并且会产生锁的性能消耗，performance_schema.threads表中查看不会。

可以使用KILL命令来终止某个线程。

```
KILL [CONNECTION | QUERY] processlist_id
```