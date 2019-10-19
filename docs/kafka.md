---
title: kafka
date: 2017-12-31 16:48:28
tags:
---
#### 一、概念
kafka，是一个分布式消息系统

#### 二、特性
1. 分布式
2. 高并发

#### 三、安装
1. kafka依赖java，所以先要安装java（忽略不讲解）
2. 去kafka官网，下载源文件
Apache官网[http://kafka.apache.org/downloads.html](http://kafka.apache.org/downloads.html)
3. 解压文件，进入目录
```
> tar zxvf kafka_2.10-0.8.2.2.tgz # 解压
> cd kafka_2.10-0.8.2.2 # 进入目录
```
3. 启动服务
3.1 启动zookeeper
启动zk有两种方式，第一种是使用kafka自己带的一个zk。
```
> bin/zookeeper-server-start.sh config/zookeeper.properties &
```
另一种是使用其它的zookeeper，可以位于本机也可以位于其它地址。这种情况需要修改config下面的sercer.properties里面的zookeeper地址
 。例如zookeeper.connect=10.202.4.179:2181
3.2 启动 kafka
```
> bin/kafka-server-start.sh config/server.properties
```

4.创建topic
```
> bin/kafka-topics.sh --create --zookeeper 10.202.4.179:2181 --replication-factor 1 --partitions 1 --topic test
```
创建一个名为test的topic，只有一个副本，一个分区。

通过list命令查看刚刚创建的topic
```
> bin/kafka-topics.sh -list -zookeeper 10.202.4.179:2181
```

5.启动producer并发送消息启动producer
```
> bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
```
启动之后就可以发送消息了
比如
test
hello boy
按Ctrl+C退出发送消息
6.启动consumer
```
> bin/kafka-console-consumer.sh --zookeeper 10.202.4.179:2181 --topic test --from-beginning
```
启动consumer之后就可以在console中看到producer发送的消息了
可以开启两个终端，一个发送消息，一个接受消息

#### 四、demo（python）