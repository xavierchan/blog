---
title: apt
toc: true
date: 2019-04-02 18:53:26
tags:
 - linux
categories:
---

### 常用指令

```shell
sudo apt-get update  更新源
sudo apt-get upgrade 更新已安装的包
sudo apt-get remove package 删除包
sudo apt-get remove package --purge 删除包，包
括配置文件等
apt-get source package  下载该包的源代码
sudo apt-get clean && sudo apt-get autoclean 清理无用的包
```

#### apt 与 apt-get 的区别

|  apt 命令 | 取代的命令  | 命令的功能  |
| :---: | :---: | :---: |
| apt install | apt-get install | 安装软件包 |
| apt remove | apt-get remove | 移除软件包 |
| apt purge | apt-get purge | 移除软件包及配置文件 |
| apt update | apt-get update | 刷新存储库索引 |
| apt upgrade | apt-get upgrade | 升级所有可升级的软件包 |
| apt autoremove | apt-get autoremove | 自动删除不需要的包 |
| apt full-upgrade | apt-get dist-upgrade | 在升级软件包时自动处理依赖关系 |
| apt search | apt-cache search | 搜索应用程序 |
| apt show | apt-cache show | 显示安装细节 |
