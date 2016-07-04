# Servlet概述

## 一、 Servlet简介

#### 1. Servlet

* Server + Applet


* 特殊的Java类（无main方法，运行于服务端，创建和销毁在服务端容器）
* Servlet与HTTP

---

## 二、Servlet处理流程分析

#### Tomcat

* Servlet容器 + 服务器

#### Servlet执行流程

* init() 只调用一次
* service() 可调用多次
* destroy() 只调用一次

#### Servlet包介绍-四个

* javax.servlet
* javax.servlet.http
* javax.servlet.annotation
* javax.servlet.descriptor

