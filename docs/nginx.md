---
title: nginx
date: 2017-12-31 23:33:53
tags:
categories:
- 笔记
---
### 概念
Nginx (engine x) 是一个高性能的HTTP和反向代理服务器，也是一个IMAP/POP3/SMTP服务器

### 常用指令
```bash
$ nginx -c /etc/nginx/nginx.conf # 配置启动
$ ./nginx -s reload # 重启
$ nginx -t # 测试配置
$ ps -ef|grep nginx 运行情况
yum install -y nodejs
```