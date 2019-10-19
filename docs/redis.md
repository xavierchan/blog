---
title: Redis
date: 2017-12-31 16:47:14
tags:
 - 缓存
categories:
 - 数据库
---

#### 一、简介

- Redis是一个开源的使用ANSI C语言编写、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。

### 一、基本概念

### 二、软件安装及目录结构

```shell
wget http://download.redis.io/releases/redis-2.8.3.tar.gz # 下载源码
tar zxvf redis-2.8.3.tar.gz # 解压
cd redis-2.8.3 # 进入目录
make # 编译
```

编译后在根目录生成src目录，有四个可执行文件

- redis-server
- redis-benchmark
- redis-cli
- redis.conf。然后拷贝到一个目录下

#### 四、配置

修改redis.conf配置文件
- 设置密码
使用命令 :/ requirepass 快速查找到 # requirepass foobared
然后去掉注释，这个foobared改为自己的密码。然后wq保存。

- 后端模式启动
修改redis.conf配置文件， daemonize yes 以后端模式启动。推荐！
打开redis.conf,使用命令 :/ daemonize 快速查找到daemonize然后修改

### 四、基本使用

```shell
redis-server redis.conf # 启动服务
redis-server start
redis-server stop
redis-server restart
redis-cli # 运行命令接口
```

#### 五、常用指令

```shell
KEYS pattern # 查找key
TYPE key # 查看类型
SET key value # 设置key
GET key # 读取key值
DEL key # 删除key
RENAME key newkey # 变更key名
MOVE key db # 移动
DUMP key # 序列化key
RANDOMKEY # 随机返回key
TTL key # 查看剩余时间(TTL, time to live)，单位秒
PTTL key # 查看剩余时间，单位毫秒
EXISTS key # 是否存在
PERSIST key # 移出过期时间，持久化
EXPIRE key seconds # 设置过期时间，以秒计
PEXPIRE key milliseconds # 设置过期时间以毫秒计。
EXPIREAT key timestamp # 设置过期时间，参数是 UNIX 时间戳
PEXPIREAT key milliseconds-timestamp # 设置过期时间，参数是 UNIX 时间戳，以毫秒计

RENAMENX key newkey
仅当 newkey 不存在时，将 key 改名为 newkey 。


# 备份
SAVE # redis 安装目录中创建dump.rdb文件

# 恢复
BGSAVE

```

#### 五、拓展
1. 防火墙开放端口
 ```
```

2. 配置自启动服务
```
> cp /usr/redis-3.0.2/utils/redis_init_script /etc/rc.d/init.d/redis # 拷贝服务脚本到系统服务目录
```

2>【开放redis端口】
**[html]** [view plain](http://blog.csdn.net/ihelloworld/article/details/7003906)[copy](http://blog.csdn.net/ihelloworld/article/details/7003906)
#关闭防火墙  

service iptables stop  

vi /etc/sysconfig/iptables  

#添加  

-A INPUT -m state --state NEW -m tcp -p tcp --dport 6379 -j ACCEPT  

#重启防火墙  

service iptables restart  

三、设置服务

    可以看到如果我们启动redis服务的话，每次都要进入到安装目录，这样是不是很繁琐，所以我们将redis做成一个服务，我们直接启动。

（设置服务前如果redis服务在开着 要先关闭redis服务 不然后面生成不了redis-6379.pid，可以查看redis服务进程 关闭杀死resid服务）
     首先将utils/redis_init_script文件复制到/etc/init.d下，同时易名为redis。执行命令

     cp  /usr/local/redis-3.0.2/utils/redis_init_script   /etc/rc.d/init.d/redis

### 六、性能优化

### 七、集群方案

### 八、面试题目

### 九、FAQ
