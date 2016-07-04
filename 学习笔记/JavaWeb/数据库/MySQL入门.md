# MySQL入门

## 一、在Mac电脑上安装MySQL

#### 1. 安装 

```
# MySQL安装
cp mysql-5.6.22-osx10.9-x86_64.tar.gz /usr/local
cd /usr/local
tar zxvf mysql-5.6.22-osx10.9-86_64.tar.gz
mv mysql-5.6.22-osx10.9-86_64 mysql #rename
rm mysql-5.6.22-osx10.9-86_64.tar.gz

cd mysql
ls -la

./scripts/mysql_install_db #init mysql

# 启动和关闭数据库
cd bin
mysqld # start mysql

ps -ef |grep mysql # 查看进程号
kill -9 xxxxx  # 结束xxxxx进程

# 数据库操作
mysql -u root -p

show databases
use xxxx
show tables
quit

```

#### 2. 便捷启动

* [XAMPP？](https://www.apachefriends.org/zh_cn/index.html)

  XAMPP是最流行的PHP开发环境

  XAMPP是完全免费且易于安装的Apache发行版，其中包含MariaDB、PHP和Perl。XAMPP开放源码包的设置让安装和使用出奇容易。

---

## 三、SQL语言简介

#### 1. SQL概述

* 过程化语言
* 非过程化语言 <- SQL

#### 2. SQL功能

* DDL

  数据定义语言

* DML

  数据操纵语言

* DCL

  数据控制语言

#### 3. SQL语言的执行方式

* 交互式SQL

  直接执行SQL语句

* 嵌入式SQL

  SQL被嵌入到高级语言

---

## 四、MySQL数据类型简介

#### 1. 整数

* TINYINT

  一个字节

* SMALLINT

  两个字节

* MEDIUMINT

  三个字节

* INT

  四个字节

* BIGINT

  八个字节

#### 2. 实数

* FLOAT

  32位

* DOUBLE

  64位

* DECIMAL

  精确的小数

  占用更多空间

#### 3. 字符串

* VARCHAR

  可变长度字符串

  节约磁盘空间、

* CHAR

  固定长度字符串

* TEXT

  字符字符串

  * TINYTEXT
  * TEXT
  * MEDIUMTEXT
  * LONGTEXT

* BLOB

  二进制字符串（字节字符串）

  * TINYBLOB
  * BLOB
  * MEDIUMBLOB
  * LONGBLOB

#### 4. 日期

* DATETIME

  八个字节

* TIMESTAMP

  四个字节

#### 5. 数据类型选择准则

* 最小原则
* 简单原则
* 避免索引列上的NULL

---

# 五、MySQL基本操作

#### 1. MySQL Workbench

