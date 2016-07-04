# JDBC 编程

## 一、JDBC简介

#### 1. JDBC概述

* ODBC（Open Database Connectivity）

  开放数据库连接

  统一的数据库接口

* JDBC（Java Data Base Connectivity）

  按照ODBC模式制定

  屏蔽不同数据库之间的差异性

#### 2. JDBC的组成

* JDBC API
  * 面向开发人员
  * 主要接口：
    * DriverManager
    * Connection
    * Statement
    * PreparedStatement
    * ResultSet
* JDBC Driver API
  * 面向低层驱动程序开发商
  * 四种类型驱动程序
    * JDBC-ODBC bridge
    * 部分java技术的本地API驱动程序
    * 全部基于java技术的本地API驱动程序
    * 全部基于java技术的本地协议驱动程序

---

## 二、JDBC编程之数据准备

---

## 三、JDBC编程之数据查询

#### 1. 下载并安装mysql-connector-java

#### 2. JDBC编程的五个步骤

* 加载驱动
* 打开连接
* 执行查询
* 处理结果
* 清理环境->关闭会话、关闭连接、完成资源的清理工作

#### 3. 编写第一个JDBC程序

alt+/ 根据输入代码提示补全

command+shift+f 格式化代码

---

## 四、JDBC编程之数据更新

---

## 五、JDBC编程之事务处理

#### 事务概述

* 事务

  操作要么都执行，要么都不执行

  事务是数据库维护数据的单位

  四个特征：

  * 原子性
  * 一致性
  * 隔离性
  * 持久性

#### 事务的语句

* 开始事务 BEGIN TRANSACTION
* 提交事务 COMMIT TRANSACTION
* 回滚事务 ROLLBACK TRANSACTION

---

## 六、编程之程序优化

#### 1. 连接管理类优化

* 工厂模式
* 单例模式

#### 2. 优化实体类

* DTO-数据传输对象 
  * 远程调用
  * 不能包含业务逻辑

#### 3. 数据库接口和实现 

DAO-数据访问对象

* 封装对数据库的访问