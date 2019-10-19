---
title: django
date: 2017-12-31 16:38:48
tags:
---
前言：
  暂时没想到有什么说的，后面补充吧。。。

## 一、Django简介

## 二、安装

```bash
$ pip install django
$ cd /root/workspace
$ django-admin.py startproject django
```

## 三、创建app
```shell
  > cd /root/workspace/django
  > python manage.py startapp blog
```

## 四、django查询常用技巧
### 1. 多表联查
两个'\_'表示关联表属性

### 2. 条件选取QuerySet
filter 表示 =
exclude 表示 !=
querySet.distinct() 去重复
\_\_exact 精确等于 like 'aaa'
\_\_iexact 精确等于 忽略大小写 ilike 'aaa'
\_\_contains 包含 like '%aaa%'
\_\_icontains 包含 忽略大小写 ilike '%aaa%'，但是对于sqlite来说，contains的作用效果等同于icontains。
\_\_gt 大于
\_\_gte 大于等于
\_\_lt 小于
\_\_lte 小于等于
\_\_in 存在于一个list范围内
\_\_startswith 以...开头
\_\_istartswith 以...开头 忽略大小写
\_\_endswith 以...结尾
\_\_iendswith 以...结尾，忽略大小写
\_\_range 在...范围内
\_\_year 日期字段的年份
\_\_month 日期字段的月份
\_\_day 日期字段的日
\_\_isnull=True/False

### 3.多个QuerySet合并

### 简化 django 开发的工具包

1. django-extensions
2. django-environ
3. django-click
4. django-fsm
5. django-contact-form
6. django-allauth
7. django-rest-auth
8. django-rest-swagger  API文档化
9. django-notifications 消息通知
10. django-activity-stream 活动流
11. django-rest-framework REST-ful API
12. django-debug-toolbar 调试工具
13. django-social-auth 社交授权认证
14. channels 即时通信
15. django-celery 定时服务
16. django-registration 注册登记？
17. django-analytical 搜索分析
18. django-robots 爬虫管控
19. django-rest-framework-jwt jwt
20. django-socketio socketio
21. django-user-accounts 账号功能，注册激活邮件等
22. django-dynamic-scraper django与scraper的集成
23. django-haystack 提供模块化搜索(elasticsearch)
24. django-configurations 组织配置？
25. django-hosts 组织host？
26. django-discover-jenkins DI

cookiecutter-django 脚手架项目
