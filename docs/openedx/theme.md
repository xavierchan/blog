---
title: 主题切换
toc: true
date: 2019-08-20 16:13:09
tags:
categories:
 - openedx
---

## edx主题切换教程

### 在配置主题前当然是阅读官方文档 [地址](https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/latest/configuration/changing_appearance/theming/index.html)

### 替换edx主题的实践

查看目前edx原来有的主题目录是 /themes
该目录下有以下内容
```
    ├── conf
    ├── dark-theme
    ├── edge.edx.org
    ├── edx.org
    ├── mytheme
    ├── open-edx
    ├── red-theme
    └── stanford-style
```
了解了这些内容后开始进行edx主题的切换[以修改studio为例子]
#### 第一步：修改环境变量 （）
```bash
cd devstack # 进入devstack目录
make dev.up # 启动服务器
make lms-shell
cd /edx/app/edxapp
vim lms.env.json
修改环境变量文件
"ENABLE_COMPREHENSIVE_THEMING": true
"COMPREHENSIVE_THEME_DIRS": [
    "/edx/app/edxapp/edx-platform/themes"
]
"THEME_NAME": "normal-theme"
```
环境变量至此配置完毕

### 第二步：重启服务并更新静态资源
```bash
cd devstack
docker-compose restart
make lms-shell # 进入lms的shell 以便执行paver 指令
cd /edx/app/edxapp/edx-platform
paver update_assets # 编译静态资源
```
如果出现访问不成功的情况可以 ```make studio-logs``` 查看相应服务器的日志信息

### 第三步：登录后台配置
访问 `http://0.0.0.0:18010/admin` 账号密码 edx/edx 登录
找到 Site themes 选项 点击进入
点击 ADD SITE THEME 按钮添加网站主题
```
Site:
Domain name: 0.0.0.0:18000
Display name: normal-theme

Theme dir name: normal-theme
```
点击save 保存成功
访问配置主题的目标网站这里是（http://0.0.0.0:18010），刷新页面发现主题配置成功！

## 回顾难点
- 需要了解docker 相关知识，edx相关配置基础
- 文档不够详尽，需要有一定知识才能够配置
- 出错信息没有明显提醒，需要了解相关知识才能自发通过日志系统查阅

## 引用参考
> [主题编译](https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/open-release-ironwood.master/configuration/changing_appearance/theming/compiling_theme.html#compiling-a-theme)
