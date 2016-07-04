# 第一章 OpenStack基本操作系统环境的PXE自动部署

## 1.1 PXE、kickstart与preseed简介

PXE是一种远程启动技术，结合CentOS的kickstart和Ubuntu的preseed机制，就可以完成自动安装操作系统的目标。

#### 1.1.1 PXE简介

* PXE是Intel公司开发的将操作系统远程下载到本地运行的一种技术。

#### 1.1.2 kickstart与preseed简介

* kickstart
  * 是Red Hat公司针对自动安装Red Hat、Fedora与CentOS这三种同一体系的操作系统而制定的问答规范。
  * 以.cfg作为文件后缀
  * 可以通过命令行工具system-config-kickstart生成
  * 也可以通过CentOS图形界面环境生成
* preseed
  * Debian/Ubuntu操作系统自动安装的问答规范。

## 1.2 PXE 服务器的准备

* 首先需要将CentOS、Ubuntu或Windows等操作系统安装光盘中的文件复制到PXE服务器中，然后当客户机通过PXE技术与服务器成功建立连接后，就可以自动引导操作系统的安装了。

#### 1.2.1 选择Ubuntu操作系统

* 选择Ubuntu作为PXE服务器的操作系统。

#### 1.2.2 Ubuntu操作系统的基本安装与更新

* Ubuntu 12.04LTS
* 配置
  * 1. 设置服务器IP地址
    2. 安装SSH Server
    3. 更新Ubuntu的源
    4. 更新系统与确认签验
    5. 安装与配置DHCP、TFTP服务
    6. HTTP服务的作用与安装
    7. kickstart与preseed配置文件的生成

## 1.3 复制Ubuntu和CentOS操作系统文件

#### 1.3.1 复制Ubuntu操作系统全目录、内核与启动镜像文件

#### 1.3.2 复制CentOS操作系统全目录、内核与启动文件

## 1.4 PXE客户端操作系统的选择与引导过程

#### 1.4.1 创建PXE客户端导示文件

#### 1.4.2 选择安装配置文件

