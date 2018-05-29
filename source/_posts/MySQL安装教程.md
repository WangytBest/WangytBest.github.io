---
title: MySQL安装教程
date: 2018-05-29 18:34:44
tags:
---

# 1. 下载安装

## 1.1 下载

MySQL8.0 For Windows zip包下载地址：[MySQL8.0 For Window](https://dev.mysql.com/downloads/file/?id=476233)，进入页面后可以不登录。后点击底部`No thanks, just start my download.`即可开始下载。或直接下载：https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.11-winx64.zip

## 1.2 安装

解压zip包到安装目录
>  配置文件：在Windows系统中，配置文件默认是安装目录下的 `my.ini` 文件（或`my-default.ini`），部分配置需要在初始安装时配置，大部分也可以在安装完成后进行更改。当然，极端情况下，所有的都是可以更改的。

>　　我们发现解压后的目录并没有`my.ini`文件，没关系可以自行创建。在安装根目录下添加 my.ini，比如我这里是：C:\Program Files\MySQL\my.ini，写入基本配置：

```
[mysqld]
# 设置3306端口
port=3306
# 设置mysql的安装目录
basedir=C:\Program Files\MySQL
# 设置mysql数据库的数据的存放目录
datadir=E:\database\MySQL\Data
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
# 默认使用“mysql_native_password”插件认证
default_authentication_plugin=mysql_native_password
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
[client]
# 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8
```
注意，里面的 basedir 是本地的安装目录，datadir 是我数据库数据文件要存放的位置，各项配置需要根据自己的环境进行配置。
查看所有的配置项，可参考：https://dev.mysql.com/doc/refman/8.0/en/mysqld-option-tables.html

# 2 初始化数据库
在MySQL安装目录的 bin 目录下执行命令：
> `mysqld --initialize --console`

执行完成后，会打印 root 用户的初始默认密码，比如：

```cmd
C:\Users\Administrator>cd C:\Program Files\MySQL\bin
C:\Program Files\MySQL\bin>mysqld --initialize --console
2018-04-28T15:57:17.087519Z 0 [System] [MY-013169] [Server] C:\Program Files\MySQL\bin\mysqld.exe (mysqld 8.0.11) initializing of server in progress as process 4984
2018-04-28T15:57:24.859249Z 5 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: rI5rvf5x5G,E
2018-04-28T15:57:27.106660Z 0 [System] [MY-013170] [Server] C:\Program Files\MySQL\bin\mysqld.exe (mysqld 8.0.11) initializing of server has completed
C:\Program Files\MySQL\bin>
```

注意！执行输出结果里面有一段： ```[Note] [MY-010454] [Server] A temporary password is generated for root@localhost: rI5rvf5x5G,E``` 其中```root@localhost:```后面的```rI5rvf5x5G,E```就是初始密码（不含首位空格）。在没有更改密码前，需要记住这个密码，后续登录需要用到。

# 3 安装数据库

在MySQL安装目录的 bin 目录下执行命令（以管理员身份打开cmd命令行，或者在安装目录Shift+右键“在此处打开命令行窗口”）：
> ```mysqld --install [服务名]```

后面的服务名可以不写，默认的名字为 mysql。

安装完成之后，就可以通过命令```net start mysql```启动MySQL的服务了。
示例：
```cmd
C:\Program Files\MySQL\bin>mysqld --install
Service successfully installed.
C:\Program Files\MySQL\bin>net start mysql
MySQL 服务正在启动 ..
MySQL 服务已经启动成功。
```

# 4 修改密码

在MySQL安装目录的 bin 目录下执行命令：
> ```mysql -u root -p```

这时候会提示输入密码，记住了上面第1.3步安装时的密码，填入即可登录成功，进入MySQL命令模式。

修改密码:
> ```ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';```

```cmd
[mysqld]
default_authentication_plugin=mysql_native_password
```

```cmd
C:\Program Files\MySQL\bin>mysql -u root -p
Enter password: ************
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.11
Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.
Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '新密码';
Query OK, 0 rows affected (0.06 sec)
mysql>
```
