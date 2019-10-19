---
title: edx学习笔记
date: 2018-05-14 11:23:28
tags:
- edx
categories:
- 笔记
---
### 序言

学习 **Open edX** ，我们需要提前准备一些知识，在具备这些知识的前提下，我们能够更好的理解和学习edx的思想和设计
比如：vagrant、paver

### 零、初步认识

**Open edX** 项目是由麻省理工学院和哈佛大学创建的，由斯坦福大学、谷歌和45所高级院校提供 支持
目前，open edx官方发布的已经有 **7个** 版本(open-release)：

- **Birch**
- **Cypress**
- **Dogwood**
- **Eucalyptus**
- **Ficus**
- **Ginkgo**
- **Hawthorn**

Open edX是个庞大而复杂的系统，笔者是因为工作原因接触的edx，他包括N个站点+N个服务结合而成，可以说是个生态也不为过(对于生态的概念认知不准确请指出)。
所以相对的，官方文档也是个相当庞大的文档体系。
edx这边提及到，如果我们是需要自己手动安装的话，需要考虑**两个点**：

1. [版本](https://openedx.atlassian.net/wiki/spaces/DOC/pages/11108700/Open+edX+Releases)
2. [方式](https://openedx.atlassian.net/wiki/spaces/OpenOPS/pages/60227779/Open+edX+Installation+Options)

像上面我提及的，edx官方发布的已经有7个版本的代码了，我们需要选择哪个版本来安装部署
另外，edx在安装方式上也提供了多种，主要有以下几点：
- **Devstack**: useful if you want to modify the Open edX code.
  - **Ginkgo** 版本及之前的，**devstack** 是个 **Vagrant** 实例。 Details are on the Running Vagrant-based Devstack page.
  - **Hawthorn** 版本, **devstack** 将基于 **Docker**. An unsupported pre-release is available. See the Docker Devstack repo for instructions.
- **Fullstack**: **Ginkgo** 版本及之前的, a Vagrant installation that mimics a production environment. Details are on the Running Fullstack page.
- **Native**: Automated installation on an Ubuntu machine of your own. Details are on the Native Open edX Ubuntu 16.04 64 bit Installation page.
- **Manual**: 手动安装，一步步执行脚本，安装依赖，配置服务
- **Bitnami**: installable pre-packaged images for popular cloud platforms. Details are at the Bitnami Open edX page.

补充上述，主要是因为笔者在学习的过程中会对不同的stack产生疑问，了解过、接触过后才有深入的了解。
一开始会有种错觉，以为Devstack只有部分服务应用，而Fullstack是全部应用，但并不是这样的，他们是你部署、配置、开发、生产一系列的工作栈
所以刚入门的菜鸟(像我一样)，要好好理解这一部分了。

基于以上，目前我们公司使用的是Ficus.1版，Devstack的版本方式安装，ok，目标明确了，那我们就开始动手吧~

### 一、安装

[安装步骤](https://openedx.atlassian.net/wiki/spaces/OpenOPS/pages/60227787/Running+Vagrant-based+Devstack)
[安装配置](http://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/latest/installation/installation_options.html#info-devstack)
对不同的工作栈，里面包含的内容不一，笔者在学习的过程中了解到，也认为这个比较重要，就给大家列出来

#### All installations include the following Open edX components:
The Learning Management System (LMS).
Open edX Studio.
Discussion Forums.
Open Response Assessments (ORA).

#### Devstack, fullstack and native installations also include:
E-Commerce
Programs
A demonstration Open edX course.
Open edX Search.

#### Fullstack and native also include the following Open edX components:
Open edX Analytics Data API.
Open edX Insights.
Certificates
XQueue, the queuing server that uses RabbitMQ for external graders.

#### Analytics devstack also includes the following Open edX components:
Open edX Analytics Data API.
Open edX Insights.
The components needed to run the Open edX Analytics Pipeline. This is the primary extract, transform, and load (ETL) tool that extracts and analyzes data from the other Open edX services.

### windows部署方案
#### 一、软件、知识准备

- virtualbox
- vagrant