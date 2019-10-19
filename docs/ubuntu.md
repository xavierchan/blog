---
title: Ubuntu
date: 2018-04-13 11:41:26
tags:
categories:
---

### 配置ssh服务

```shell
sudo apt-get update
sudo apt-get install openssh-server
ps -e | grep ssh # sshd 为 服务端，ssh-client 为客户端
```

## ufw

ubuntu的防火墙服务
sudo ufw allow 3307 # 直接开启端口

### 安全

官方认可的 Ubuntu 安全更新只经由 [security.ubuntu.com](security.ubuntu.com) 发布。

您可以使用以下列表中的任何一个源镜像只要往您的 /etc/apt/sources.list 文件中像下面这样添加一行:

```list
deb http://security.ubuntu.com/ubuntu xenial-security main
```
