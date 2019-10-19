---
title: docker-machine
date: 2018-02-03 15:37:14
tags:
categories:
---
Docker Machine 是 Docker 官方编排（Orchestration）项目之一，负责在多种平台上快速安装 Docker 环境。
意思就是使用一台机器，对自己的资产进行管理

##
```bash
$ curl -L https://github.com/docker/machine/releases/download/v0.13.0/docker-machine-`uname -s`-`uname -m` >/usr/local/bin/docker-machine && \
  chmod +x /usr/local/bin/docker-machine # mac
$ curl -L https://github.com/docker/machine/releases/download/v0.13.0/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine && \
sudo install /tmp/docker-machine /usr/local/bin/docker-machine # linux
$ docker-machine version # 安装后检查是否成功
$ docker-machine ls # 虚拟机
$ docker-machine create --driver virtualbox default # 创建虚拟机
$ docker-machine env default # 获取虚拟机环境切换命令
$ eval $(docker-machine env default) # 连接到vm
$ docker-machine stop default
$ docker-machine start default

- `docker-machine config`
- `docker-machine env`
- `docker-machine inspect`
- `docker-machine ip`
- `docker-machine kill`
- `docker-machine provision`
- `docker-machine regenerate-certs`
- `docker-machine restart`
- `docker-machine ssh`
- `docker-machine start`
- `docker-machine status`
- `docker-machine stop`
- `docker-machine upgrade`
- `docker-machine url`
```

分布式，分开部署的方式
