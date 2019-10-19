---
title: Open edX 安装
toc: true
date: 2019-04-01 22:15:44
tags:
categories:
 - openedx
---
### 序言
该篇章主要以全局的角度，引导大家如何搭建公司的edx项目环境，以及开发调试的配置。
该篇章中提及到的相关技术或edx源码相关的(如：版本、devstack的理解)，请到上一篇 **[行者入坑](/blogs/6)** 。
先阅读该篇章并不影响环境的搭建，但如果有上一篇章的基础，会更加深入和顺利。

### 一、预装环境
- **[virtualbox](https://virtualbox.org)** 4.3.12或以上
- **[vagrant](https://vagrantup.com)** 1.6.5或以上
安装步骤不多说，请自行安装

### 二、版本与方式
基于工作原因，我们选择以下方式：
- 版本：**Ficus.1**
- 方式：**vagrant**， **virtualbox**

### 三、安装Devstack
##### 1. 创建 **devstack** 目录
```shell
$ mkdir devstack
$ cd devstack
```
##### 2. 下载 **[Vagrantfile](https://raw.githubusercontent.com/edx/configuration/open-release/ficus.1/vagrant/release/devstack/Vagrantfile)** 到devstack目录
##### 3. 启动并初始化box，并为edxapp用户设置密码
```shell
$ vagrant up
$ vagrant ssh
$ sudo passwd edxapp
```

### 四、pycharm安装及远程调试配置
1. 网上下载pycharm 2018.xx，安装并激活
2. 打开edx-platform项目
3. 菜单 File -> Settings 打开设置
4. 打开 Project edx-platform -> ProjectInterpreter
5. 右边设置添加一个虚拟机的python解析器
6. 添加 SSH Interpreter
  HOST：127.0.0.1
  Port：2222
  Username：edxapp
7. 根据引导，输入登录密码，配置文件目录映射
8. 添加环境变量
  到svn **99 系统发布与运维 -> 环境变量** 目录下，把所有 **json配置** 拷贝到虚拟机中 **/edx/app/edxapp** 目录下
9. 迁移mongodb、mysql
10. 执行指令，更新数据库及依赖
11. 配置某一项目的运行配置
  Run/Debug Configurations
  Script path：./manage.py
  Parameters：lms runserver --settings=devstack 0.0.0.0:8000
  Working dir：项目本地目录
  Path mappings：目录映射
以上操作已经把edx的环境已经配置完毕了。

### 补充、数据库迁移
#### mongodb
1. 拷贝mongo备份文件到虚拟机
```shell
$ scp eliteu@192.168.0.101:/home/eliteu/data_back/101/mongo.tar.gz ./
```
可以通过edx-platform目录共享的方式移动到虚拟机，然后解压
2. 到虚拟机里，执行指令，恢复mongodb
```shell
$ mongorestore -h<localhost> -d edxapp -u edxapp -p <password> --dir=<path> --drop
```
--dir 备份文件的目录
--drop 先删除已存在的数据库，再进行恢复

#### mysql
##### 1. 拷贝mysql备份文件到虚拟机
可以通过edx-platform目录共享的方式移动到虚拟机，然后解压
##### 2. 到虚拟机里，执行指令，恢复mysql
```shell
# edx包含以下数据库：analytics-api、dashboard、discovery、ecommerce、edxapp、edxapp_csmh、programs、reports、xqueue
# 不过目前主要用到edxapp，其他可以先忽略
mysql -hlocalhost -uroot -p # 进入数据库
mysql> show databases; # 查看数据库
mysql> drop database `edxapp`;
mysql> create database `edxapp` DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
$ gunzip < beta_edxapp.sql.gz | mysql -u<username> -p<pwd> <dbname>
```
注意：备份是来自beta环境的数据库，数据库名称是修改过的，根据个人情况，调整数据库名称，edxapp=beta_edxapp

## 参考资料

> - []()
> - []()
