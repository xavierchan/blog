---
title: MongoDB
toc: true
date: 2019-04-02 19:09:19
tags:
categories:
- 数据库
---

MongoDB是一个NoSQL数据库系统：一个数据库可以包含多个集合（Collection），每个集合对应于关系数据库中的表；而每个集合中可以存储一组由列标识的记录，列是可以自由定义的，非常灵活，由一组列标识的实体的集合对应于关系数据库表中的行。

### 前言

复习纲要

- 安装及文件目录等
- 用户权限
- 常用指令
- 性能指标观察
- 性能优化经验
- 集群经验

### 一、基本概念

|数据类型|描述|
|:---:|:---:|
|String|字符串。存储数据常用的数据类型。在 MongoDB 中，UTF-8 编码的字符串才是合法的。|
|Integer|整型数值。用于存储数值。根据你所采用的服务器，可分为 32 位或 64 位。|
|Boolean|布尔值。用于存储布尔值（真/假）。|
|Double|双精度浮点值。用于存储浮点值。|
|Min/Max keys|将一个值与 BSON（二进制的 JSON）元素的最低值和最高值相对比。|
|Array|用于将数组或列表或多个值存储为一个键。|
|Timestamp|时间戳。记录文档修改或添加的具体时间。|
|Object|用于内嵌文档。|
|Null|用于创建空值。|
|Symbol|符号。该数据类型基本上等同于字符串类型，但不同的是，它一般用于采用特殊符号类型的语言。|
|Date|日期时间。用 UNIX 时间格式来存储当前日期或时间。你可以指定自己的日期时间：创建 Date 对象，传入年月日信息。|
|Object ID|对象 ID。用于创建文档的 ID。|
|Binary Data|二进制数据。用于存储二进制数据。|
|Code|代码类型。用于在文档中存储 JavaScript 代码。|
|Regular expression|正则表达式类型。用于存储正则表达式。|

### 二、软件安装及目录结构

#### 2.1 源码安装

```shell
# 第一步： 构建mongodb的文件目录
mkdir /root/software
mkdir /root/software/mongodb
mkdir /root/software/mongodb/data
mkdir /root/software/mongodb/logs

# 第二步： 访问 [mongodb官网](https://www.mongodb.com) 选择linux版本，下载源码
cd /root/software/mongodb
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.4.3.tgz
tar zxvf mongodb-linux-x86_64-3.4.3.tgz

# 第三步：初始化配置文件
touch logs/mongodb.log
touch mongodb.conf

# 第四步：以配置文件方式，运行mongodb
cd mongodb-linux-x86_64-3.4.3/bin
./mongod --config /root/software/mongodb/mongodb.conf
```

#### 2.2 Docker安装

```shell
# 1. 拉取镜像
docker pull mongo:4.0-rc

# 2. 运行容器
docker run --name mongo -d -v /my/own/datadir:/data/db mongo:4.0-rc
```

#### 2.3 目录结构

```js
/root
  |--software
  |   |--mongodb
  |       |--data
  |       |--logs
```

### 三、运维常用

在安装MongoDB后，启动服务器进程（mongod），可以通过在客户端命令mongo实现对MongoDB的管理和监控。输入mongo可以查看最顶层命令。

### 四、基本使用

```sql
db.serverStatus() # 查看数据库服务器的状态
db.hostInfo()
db.version()
show log
db.stats() # 查看数据库统计信息
db.repairDatabase()

mongod--repair --dbpath /var/lib/mongodb/ --repairpath /var/lib/mongodb/test /

6、db.getCollectionNames() # 查看集合名称列表


# 数据库管理
show dbs # 查看数据库
use one_database # 使用某个数据库
db.dropDatabase() # 删除数据库

# 集合管理
show collections # 查看集合
db.createCollection(name, { size : ..., capped : ..., max : ... } ) # 创建集合
db.one_collections.drop() # 删除集合

# 数据管理
db.one_collections.insert({'version':'3.5', 'segment':'e3ol6'}) # 增
db.one_collections.remove({'version':'3.5'}) # 删
db.one_collections.remove({}) # 删除所有
db.one_collections.update(<query>, <update>, <options>) # 改
db.one_collections.find().sort({KEY: 1(-1)}) # 查
db.one_collections.findOne({'version':'3.5'}) # 查询
db.baseSe.count() # 统计集合记录数

# 数据备份
命令格式：mongodump -h dbhost -d dbname -o dbdirectory
-o: 备份的数据存放的位置，例如：/home/bak

# 数据恢复
命令格式：mongorestore -h dbhost -d dbname -dorectoryperdb dbdireactory

-directoryperdb: 备份数据所在位置，例如：/home/bak/test
-drop: 加上这个参数的时候，会在恢复数据之前删除当前数据；

公共参数
-h: mongodb所在服务器地址，例如127.0.0.1，也可以指定端口:127.0.0.1:8080
-d: 需要备份(恢复)的数据库名称，例如：test_data；恢复时，可以跟原来备份的数据库名称不一样
-u: 用户名称，使用权限验证的mongodb服务，需要指明导出账号
-p: 用户密码，使用权限验证的mongodb服务，需要指明导出账号密码

# 常用shell
mongodb://admin:123456@localhost/db

```

### 五、权限管理

### 六、性能优化

### 七、集群方案

### 八、面试题目

### 九、FAQ
