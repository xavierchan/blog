---
title: celery学习笔记
date: 2018-04-28 10:21:36
tags:
- celery
categories:
- 笔记
---

### 序言

celery是一个基于django的分布式任务调度处理库，支持rabbitMQ、redis、数据库作为任务队列

### 特点

2.Celery特点：

- 简单，易于使用和维护，有丰富的文档
- 高效，单个 Celery 进程每分钟可以处理数百万个任务（并发2w）
- 灵活，Celery 中几乎每个部分都可以自定义扩展
- Celery 非常易于集成到一些web开发框架中

4.Celery组成结构

- 任务队列是一种跨线程、跨机器工作的一种机制
- 任务队列中包含任务的工作单元。有专门的工作进程持续不断的监视任务队列，并从中获得新的任务并处理
- Celery通过消息进行通信，通常使用一个叫broker(中间人)来协client(任务的发出者)和worker(任务的处理者)
- client发出消息到队列中，broker将队列中的信息派发给worker来处理
- 一个Celery系统可以包含很多的worker和broker，可增强横向扩展性和高可用性能。
- Celery组成结构是生产者消费者模型的一种体现

### Application

首先，我们需要创建celery实例，它是一个应用
对于django项目，一般会在app下面建立task.py文件，用来创建任务和管理worker

### broker

broker其实就是队列，在broker选择上

|名称|状态|监视|远程控制|
| :---: | :---: | :---: | :---: |
|RabbitMQ|稳定|是|是|
|Redis|稳定|是|是|
|Mongo DB|实验性|是|是|
|Beanstalk|实验性|否|否|
|Amazon SQS|实验性|否|否|
|Couch DB|实验性|否|否|
|Zookeeper|实验性|否|否|
|Django DB|实验性|否|否|
|SQLAlchemy DB|实验性|否|否|
|Iron MQ|实验性|否|否|

稳定支持的有Rabbimq和Redis，而Redis可能存在断电时丢消息，所以官方也推荐broker选择RabbitMQ

### backend

用于存储这些消息以及celery执行的一些消息和结果。一般情况下我们选择Mysql作为backend。

## 任务类型

|案例|频率|耗时|事务|事件|
| :---: | :---: | :---: | :---: | :---: |
|1|高|长|无|
|1|高|长|有|
|1|高|短|无|小文件上传、邮件发送、短信发送|
|1|高|短|有|订单提交|
|1|低|长|无|大文件上传|
|1|低|长|有|
|1|低|短|无|访问计数|
|1|低|短|有|

## 队列创建依据

- 业务或功能较为重要，单独一个 Queue
- 基础服务，频率高，耗时短的，可以用同一个 Queue

### 实用参数

``` shell
-A ${app_name} worker # 运行哪个应用
-B # beat模式
-Q q1,q2 # 指定队列
--autoscale=10,3 # 最小三个进程，最多10个进程
```

## 注意事项

1. celery worker 启动时，如果是root用户，需要设置环境变量：

``` shell
$ export C_FORCE_ROOT='true'
```

1. Celery4.x 开始不再支持Windows平台，如果需要在Windows开发，请使用3.x的版本。
2. 使用 RabbitMQ 或 Redis 作为 Broker，生产环境永远不要使用关系数据库
3. 不要使用复杂对象作为任务函数的参数
