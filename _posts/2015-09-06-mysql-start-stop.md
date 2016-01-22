---
layout: post
title:  "MySQL启动/停止/重启服务"
date: 2015-03-09 12:21:49
categories: MySQL
tags: MySQL
---

如何启动，停止，重启MySQL服务。


## 一、启动 ##

1. 使用 service 启动：service mysqld start
2. 使用 mysqld 脚本启动：/etc/inint.d/mysqld start
3. 使用 safe_mysqld 启动：safe_mysqld &

## 二、停止 ##

1. 使用 service 停止：service mysqld stop
2. 使用 mysqld 脚本停止：/etc/inint.d/mysqld stop
3. mysqladmin shutdown


## 三、重启 ##

1. 使用 service 重动：service mysqld restart
2. 使用 mysqld 脚本重动：/etc/inint.d/mysqld restart


----------


查看MySQL服务进程是否启动：

```
ps -aux | grep mysqld
```

查看MySQL是否正常监听端口：

```
netstat -nltp| grep mysql

```

