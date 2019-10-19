---
title: vagrant
date: 2018-05-24 14:21:57
tags:
categories:
---

```shell
$ mkdir proj && cd proj # 创建项目目录
$ vagrant init          # 初始化，创建后会生成Vagrantfile，所有项目的根目录、网络配置、数据卷挂载都在这里(注意，因为数据卷挂载，如果rm -rf的话会删除)
$ vagrant up            # 启动虚拟机
$ vagrant ssh           # 进入虚拟环境
$ vagrant suspend       # 睡眠
$ vagrant halt          # 关机
$ vagrant destroy       # 销毁
```

### Boxes
何为box？在vagrant的世界里，如果你知道docker，那么他就是docker世界里的 “images” ，其实就是某个版本的虚拟机的快照

### 同步文件夹
vagrant ssh进入系统后，其实是以vagrant用户登录了虚拟机
而 /home/vagrant 目录正是我们挂载的项目目录，所有修改都会同步，我们可以在本机开发，虚拟机运行