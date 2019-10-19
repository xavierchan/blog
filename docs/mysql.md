---
title: Mysql
date: 2017-12-31 16:48:49
tags:
categories:
- 数据库 
---

## 一、软件
### 1. 安装
yum install mysql

### 2. 软件表结构
mysql安装完毕后，会有个“mysql”的数据库，用于存储权限表，我们也通过这些权限表来实现权限管理的
#### 2.1 user表
user表用于记录允许连接到服务器
##### 2.1.1 用户列
- host 主机名(%为所有)
- user 用户名
- password 密码
登录时，根据这三个字段进行判断
创建时，只需这三个字段
修改密码也只用这三个字段

##### 2.1.2 权限列
- Grant_priv 是否有Grant权限
- Shutdown_priv 是否有停止mysql服务的权限
- Super_priv 是否有超级权限
- Execute_priv 是否有执行存储过程和函数的权限
包含普通权限:查询权限、修改权限等 操作数据库的动作；
包含高级管理权限:关闭服务权限、超级权限、加载用户等 管理数据库的动作；
这些字段只有N和Y两个选项，为安全起见默认值都设为N；
对这些权限的管理可以使用GRANT语句、也可以通过UPDATE user表的这些列来实现。

##### 2.1.3 安全列
##### 2.1.4 资源控制列
- max_questions 每小时允许执行多少次查询
- max_updates 每小时允许执行多少次更新
- max_connections 每小时允许建立多少连接
- max_user_connections 单个用户可以同时具有的连接数
这些字段默认值为0，表示没有限制

#### 2.2 db表
##### 2.2.1 用户列
- Host   主机名
- Db      数据库名
- User   用户名

##### 2.2.2 权限列

#### 2.3 tables_priv表
单表权限控制
#### 2.4 columns_priv表
单列权限控制

#### 2.5 procs_priv表
存储过程、存储函数权限控制
- Host                 主机名
- Db                    数据库名
- User                 用户名
- Routine_name 存储过程/存储函数的名字
- Routine_type   标识它是FUNCTION(存储函数)还是PROCEDURE(存储过程)
- Proc_priv         拥有的权限(Execute、Alter Routine、Grant)
- Timestamp       更新的时间
- Grantor            权限是谁设置的

#### 2.6 用户的权限分配规则
1. Mysql的权限分配是按照user表--->db表--->tables_priv表--->columns_priv表的顺序进行分配的
2. 如果user表中某一权限的值为Y，就不需要检查往后的表了
3. 如果user表中某一权限的值为N，则依次往后检查每一张表

4. 服务指令
```
$ service mysqld restart
$ service mysqld start
$ service mysqld stop
```

## 二、权限、设置
### 1. 权限
```sql
create user username identified by 'password';
show grants for root@'localhost'; # 查看用户权限
select  *  from  mysql.user  where  User='username'  and  Host='hostname'
revoke all privileges, grant option from 'username'@'hostname'; # 取消全部权限
flush privileges; # 刷新权限
drop user username @ localhost;
```

### 2. 字符集
```sql
修改数据库字符集：
alter database db_name default character set character_name [collate ...];
把表默认的字符集和所有字符列（CHAR,VARCHAR,TEXT）改为新的字符集：
alter table logtest convert to character set utf8 collate utf8_general_ci;
只是修改表的默认字符集：
alter table logtest default character set utf8 collate utf8_general_ci;
修改字段的字符集：
alter table logtest change title title varchar(100) character set utf8 collateutf8_general_ci;
查看数据库编码：
show create database db_name;
查看表编码：
show create table tbl_name;
查看字段编码：
show full columns from tbl_name;
```

## 三、应用
### 1. 常用指令
```sql
> show databases;
> use databaseName;
> show tables;
> show create table 表名;
create database `education_live` default character set utf8 collate utf8_general_ci; # 创建数据库
create user 'education_live'@'%' identified by 'education_live'; # 创建用户
grant all privileges on education_live.* to 'education_live'@'%' identified by 'education_live'; # 权限配置
flush privileges; # 刷新权限
```

## 四、有用功
```sql
$ show global variables like "%datadir%" # 查看数据文件物理位置
```
\G是格式化输出

连接
连接时如果不带host参数，默认是localhost，这时用户登录会查找 user=用户名，host=loaclhost 的用户进行身份验证
如果只创建了host=%的用户，只能用-h127.0.0.1来访问

```

## 四、有用功
### 4.1 查看数据文件的物理位置
```sql
$ show global variables like "%datadir%" # 查看数据文件物理位置
```
\G是格式化输出
### 4.2 用户远程连接
连接
连接时如果不带host参数，默认是localhost，这时用户登录会查找 user=用户名，host=loaclhost 的用户进行身份验证
如果只创建了host=%的用户，只能用-h127.0.0.1来访问

### 4.3 远程连接限制
my.cnf配置文件
bind_address 127.0.0.1
该配置设置回环地址，地址只能为本机，如果需要远程连接，必须注释掉

#### mysqldump(备份)
命令格式：mysqldump -h主机名  -P端口 -u用户名 -p密码 –database 数据库名 > 文件名.sql
