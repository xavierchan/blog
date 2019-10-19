---
title: SMTP协议
toc: true
date: 2019-08-29 12:24:43
tags:
categories:
  - 网络协议
---
简单邮件传输协议 (Simple Mail Transfer Protocol, SMTP) 是在Internet传输email的事实标准。
SMTP是一个相对简单的基于文本的协议。在其之上指定了一条消息的一个或多个接收者（在大多数情况下被确认是存在的），然后消息文本会被传输。可以很简单地通过telnet程序来测试一个SMTP服务器。SMTP使用TCP端口25。要为一个给定的域名决定一个SMTP服务器，需要使用MX (Mail eXchange) DNS。

当前的反垃圾邮件技术可以分为4大类：过滤器（Filter）、反向查询(Reverse lookup)、挑战(challenges)和密码术(cryptography),这些解决办法都可以减少垃圾邮件问题，但是都有它们的局限性。
