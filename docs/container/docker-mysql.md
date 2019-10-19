---
title: docker常用容器配置
date: 2018-02-02 09:40:25
tags:
categories:
- 有用功
---

## 一、mysql容器
```bash
$ docker pull mysql:5.6 # 拉取镜像
$ docker run -d --name docker-mysql -v <local_path>:<docker_path> -e MYSQL_ROOT_PASSWORD=<root_pwd> -p 3308:3306 mysql # 运行容器
$ docker exec -t -i mysql /bin/bash # 进入容器
select user, host from user;
create database education_live default character set utf8 collate utf8_general_ci;
grant all on education_live.* to 'education_live'@'%' identified by 'educationlive'; # 创建应用连接账号，并设置权限
```
docker run -d --name mysql \
-v /root/docker/mysql/congfig:/etc/mysql/conf.d \
-v /root/docker/mysql/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=CZX764545 \
mysql:5.6


```bash
-d : --detach，后台运行。
--name : 为你的镜像创建一个别名，该别名用于更好操作。
-p : 映射端口，一般我们会将默认端口进行更改，避免与本机的mysql端口冲突，如果你宿主机有mysql，请更改端口，如 -p 33060:3306。
-e : 环境变量。为mysql的root用户设置密码为123456。
-v : 指定数据卷，意思就是将mysql容器中的/var/lib/mysql（这个是数据库所有数据信息文件）映射到宿主机/data/mysql里面。
-i : --interactive，交互界面。
-t : --tty，伪终端界面。
```

## 二、redis容器
```bash
$ docker pull redis:4.0.7 # 拉取镜像
$ docker run -d --name docker-redis -p 6379:6379 -v <pwd>/redis.conf:/etc/redis/redis.conf -v <local_path>:<docker_path> redis:4.0.7 redis-server --appendonly yes # 运行容器
$ docker exec -it docker-redis redis-cli # 运行客户端
```

## 三、python2.7容器
```bash
$
```