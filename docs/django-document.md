---
title: django-document
toc: true
date: 2019-04-02 19:39:39
tags:
categories:
 - 笔记
---
django的admin document其实也不是什么稀奇的东西，但可能我们会忽略掉，详情请看 [官方文档](https://docs.djangoproject.com/en/1.11/ref/contrib/admin/admindocs/)

#### 问题情况

- url太多，各种各样的引入方式，甚至通过外部模块安装，查找麻烦
- 数据库表没有注释，不清楚是什么意思
- 模板引擎标签记不得

#### 安装步骤

1. 加入 **django.contrib.admindocs** 到你的 **INSTALLED_APPS**；
2. 加入 url(r'^admin/doc/', include('django.contrib.admindocs.urls')) 到你的 **urls.py** 中(建议跟着/admin后面)
3. 安装docutils Python模块 [http://docutils.sf.net/](http://docutils.sf.net/)

#### 安装结果

1. 得到完整的 **路由表** (包括外部安装的app)
2. 得到完整的 **数据库模型** (比看数据库更为详细清晰，在结构方面)
3. 可查看目前可使用的所有 **模板标签**
