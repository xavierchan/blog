---
title: RabbitMQ
date: 2018-05-01 15:34:16
categories:
 - 数据库
---

- 4369 (epmd), 25672 (Erlang distribution)
- 5672, 5671 (AMQP 0-9-1 without and with TLS)
- 15672 (if management plugin is enabled)
- 61613, 61614 (if STOMP is enabled)
- 1883, 8883 (if MQTT is enabled)

## 4369 (epmd), 25672 (Erlang distribution)

Epmd 是 Erlang Port Mapper Daemon 的缩写，在 Erlang 集群中相当于 dns 的作用，绑定在4369端口上。

## 5672, 5671 (AMQP 0-9-1 without and with TLS)

AMQP 是 Advanced Message Queuing Protocol 的缩写，一个提供统一消息服务的应用层标准高级消息队列协议，是应用层协议的一个开放标准，专为面向消息的中间件设计。基于此协议的客户端与消息中间件之间可以传递消息，并不受客户端/中间件不同产品、不同的开发语言等条件的限制。Erlang 中的实现有 RabbitMQ 等。

## 15672 (if management plugin is enabled)

通过 http://serverip:15672 访问 RabbitMQ 的 Web 管理界面，默认用户名密码都是 guest。（注意：RabbitMQ 3.0之前的版本默认端口是55672，下同）

## 61613, 61614 (if STOMP is enabled)

Stomp 是一个简单的消息文本协议，它的设计核心理念就是简单与可用性，官方文档，实践一下 Stomp 协议需要：
一个支持 stomp 消息协议的 messaging server (譬如activemq，rabbitmq）；
一个终端（譬如linux shell);
一些基本命令与操作（譬如nc，telnet)

## 1883, 8883 (if MQTT is enabled)

MQTT 只是 IBM 推出的一个消息协议，基于 TCP/IP 的。两个 App 端发送和接收消息需要中间人，这个中间人就是消息服务器（比如ActiveMQ/RabbitMQ），三者通信协议就是 MQTT
