---
title: 独立app
toc: true
date: 2019-04-09 08:16:26
tags:
categories:
- openedx
---

#### [cookiecutter(传送门)](https://github.com/audreyr/cookiecutter)

> Cookiecutter 是通过一个项目模板来创建项目。比如：Python软件包

#### [cookiecutter-django-app(传送门)](https://github.com/edx/cookiecutter-django-app)

openedx在开放以来，构建的社区和体系都是非常完善健全的，当然包括开发者使用的一系
列工具，这个项目主要是一个符合edx项目架构风格的django app脚手架工具

通过指令，设置项目相关的信息，即可获得一个独立的django app项目，可见他的目录是非
常健全的，涵盖到文档、测试、作者信息等等

在edx一个实例中，无论是vagrant还是docker，开发栈总会为我们预留src这个目录，他的
意图就是让我们能否在此目录，集成和开发通过cookiecutter工具创建的django app

### 一、安装依赖

#### 本地

```shell
pip install xlrd
pip install -e /edx/src/elitemba
```

#### 生产

```shell
pip install xlrd
pip install git+https://github.com/xavierchan/elitemba.git
```
