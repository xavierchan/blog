---
title: openedx-develop
toc: true
date: 2019-08-20 16:15:23
tags:
categories:
 - openedx
---

### 前言
> Open edX 是个庞大且复杂的分布式系统，其中涵盖了许多巧妙而独特的设计，为了统一开发风格与方式，以及跟随edx的步伐，协同开发，减少官方代码的hack，故整理本文开发指引，请开发者仔细阅读

### 一、前端代码修改
> 为了让社区开发者更好的实现其独特的业务功能，edx设计了 **主题功能** ，其设计目的在于，通过选择使用同等目录的文件来实现个性化代码

主题项目包含以下内容：
- **edx-platform/lms/templates/**
- **edx-platform/lms/statics/images/**
- **edx-platform/lms/statics/sass/**
- **edx-platform/cms/templates/**
- **edx-platform/cms/statics/images/**
- **edx-platform/cms/statics/sass/**

#### 开发方式：
1、创建主题项目；
2、**通过创建相同位置的模板、静态资源，实现开发者自定义的页面交互功能**
3、为edx实例配置主题功能
ps. 以上，已经可以覆盖大部分页面和功能修改了，包括 **邮件模板** 等

#### 例子：
- edx主题切换 [**链接**](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=71)
- eduNext 已经通过主题功能，提供了各种自定义业务需求 [**链接**](https://github.com/eduNEXT?utf8=%E2%9C%93&q=theme&type=&language=)

### 二、edx插件系统
> edx本身设计了一套**插件系统**，让开发者开发的**第三方app**无需在edx-platform中添加任何代码，即可集成到LMS或Studio中，
新增的业务功能代码，可以通过此方式编写，除非有业务功能交叉，否则代码十分干净，完全不会hack官方代码

#### 开发方式：
详情请查阅文档  [**插件开发方式**](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=158)

#### 例子：
- appsember的figures [**链接**](https://github.com/appsembler/figures)

### 三、开源项目的二次开发
> edx项目中使用了许多开源项目，其中包括social auth等，edx官方对这些开源项目的做法是fork，做自己的代码修改

#### 开发方式：
1、Fork原开源项目仓库，进行分支建立并二次开发；
2、修改edx-platform依赖文件，替换成我们自己二次开发的仓库
#### 例子：
- qq auth backend

### 四、主题项目独立翻译(待实验)
> 针对以上主题模式的开发，对主题模板内容单独托管翻译文件，edx官方翻译+主题翻译相互作用，完成多语言功能

#### 优点
- 部分edx官方的po、mo文件无需修改
- 个性化翻译得到分离，减少维护范围，可控性更高

### 引用参考
> [edx 变更主题（官方）](https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/open-release-ironwood.master/configuration/changing_appearance/theming/index.html)



## 参考资料
> - []()
> - []()
