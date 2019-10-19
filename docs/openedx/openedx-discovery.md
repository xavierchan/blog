---
title: Discovery
toc: true
date: 2019-08-20 16:14:20
tags:
categories:
 - openedx
---
# Discovery

**discovery 是一种服务，可以访问整合的课程和程序元数据。它主要通过支持课程，课程运行，程序，目录和搜索的REST API来实现。**


## 介绍

Discovery允许Open edX安装内部的服务使用整合的元数据源以呈现给用户。
Discovery还允许外部各方以安全的方式从单个中央位置访问Open edX安装中的内容数据。

<br>

- Course and Course Runs
`course-v1:foo+bar+fall` 和 `course-v1:foo+bar+spring` 都是 course-v1:foo+bar

<br>

- Catalogs
Catalogs 是自定义的一个课程组，作为 elasticsearch 提供的查询字段

<br>
- Programs
Programs是固定的课程集合，其完成导致授予证书

<br>
- Data Loading
数据收集管道：通过 `refresh_course_metadata` 的命令运行，从 cms、lms、ecommerce、marketing site 收集 course 和 course run的信息

<br>
- Search
Discovery使用Elasticsearch来索引有关课程，课程和程序的数据。
可以使用 `update_index` 的管理命令随时更新索引。
Discovery API可用于针对Elasticsearch索引运行搜索查询。


---
## 一、技术栈

course-discovery app 作为聚合服务
elasticsearch 作为数据索引，对外提供接口

---
## 二、运行环境
- 环境变量 - DISCOVERY_CFG - /edx/etc/discovery.yml
- 虚拟环境 - VIRTUAL_ENV - /edx/app/discovery/venvs/discovery
- django settings - DJANGO_SETTINGS_MODULE

- python3
- django

---
## 三、相关功能

edX数据的分布随着时间的推移而增长。 
edx.org上的任何给定功能可能需要来自Studio，LMS，电子商务服务和营销网站的信息。
Discovery是一个数据聚合器，其工作是收集，整合和提供对这些服务的信息的访问。

### 概念
parnter：合作伙伴，设置成功之后，可以拉取partner 的 course 和 course run信息。
organizations：课程的所属组织，创建课程时的必填字段
people：个人的信息，关联到organization、partner（直接在admin填写即可，无特殊含义字段）
credit：学分 （需要在 lms 配置 credit provider）
publisher：一种信息管理工具，旨在支持课程编写，审核和批准工作流程。该工具可用于管理课程元数据，与营销网站一起使用

### 使用
Discovery OIDC 配置：http://pms.elitemc.cn/index.php?m=doc&f=view&docID=201
Program 创建及字段详解：http://pms.elitemc.cn/index.php?m=doc&f=view&docID=200
Program命令 （discovery 更新课程信息和 lms 更新 program缓存）：http://pms.elitemc.cn/index.php?m=doc&f=view&docID=228
Partner 配置：http://pms.elitemc.cn/index.php?m=doc&f=view&docID=227



---
## 四、相关脚本

更新 discovery 的课程信息：`refresh_course_metadata`
更新 elasticsearch 的索引：`update_index`


---
## 五、发布相关

---
## 六、常见问题

- lms 后台 catalog integration 对应的用户不存在，更换成 `discovery_worker` 即可

---
## 七、引用参考

官方文档：https://edx-discovery.readthedocs.io/en/latest
api文档：http://discovery.eliteu.xyz/api-docs




## 参考资料
> - []()
> - []()
