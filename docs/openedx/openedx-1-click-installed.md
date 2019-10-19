---
title: 一键安装 - Tutor
toc: true
date: 2019-04-09 00:37:32
tags:
 - openedx
 - docker
categories:
 - openedx
 - 优秀项目
---
#### 1 安装
```shell
sudo curl -L "https://github.com/regisb/tutor/releases/download/latest/tutor-$(uname -s)_$(uname -m)" -o /usr/local/bin/tutor
sudo chmod +x /usr/local/bin/tutor
```

#### 2 项目创建
tutor local quickstart

#### 3 项目文件
项目创建后，tutor会为我们创建以下软件目录 /Library/Application Support/tutor
如果不清楚可以通过命令tutor config printroot 查看
```
tutor
    ├── config.yml
    ├── data
    ├── env
```
- config.yml
tutor的配置文件，在创建项目时会根据此文件进行交互式配置
- data
tutor以数据卷挂载的方式，将容器内的mysql、mongodb、staticfiles、uploads等持久化到本地，即使容器被破坏了，重建数据仍在
- env
该目录下主要是不同环境的docker-compose文件，env和data尤为重要，尤其是我们对其二次开发，将ecommerce、inside等安装配置时用到

## 参考资料
> - [tutor docs](https://docs.tutor.overhang.io)
> - [tutor github](https://github.com/regisb/tutor)

