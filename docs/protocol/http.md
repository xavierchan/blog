---
title: HTTP协议
toc: true
date: 2019-04-01 22:22:54
tags:
categories:
 - 网络协议
---

## http请求

1. 无连接，完成请求即断开
2. 媒体独立
3. 无状态

---

1. 请求行
2. 请求头部
3. 空行
4. 请求数据

## http响应

1. 状态行
2. 消息报头
3. 空行
4. 响应正文

## 请求方法

| 方法 | 版本 | 描述 |
| :---: | :---: | :---: |
| GET | 1.0 | 请求指定的页面信息，并返回实体主体。 |
| POST | 1.0 | |
| HEAD | 1.0 | |
| PUT | 1.1 | |
| PATCH | 1.1 | |
| DELETE | 1.1 | |
| OPTIONS | 1.1 | |
| CONNECT | 1.1 | |
| TRACE | 1.1 | |

## 参考资料