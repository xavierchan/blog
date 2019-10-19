---
title: Insights
toc: true
date: 2019-04-09 00:30:20
tags:
 - openedx
 - hadoop
categories:
 - openedx
 - 安装与配置
---

## 一、技术栈

- analytics dashboard 【[github](https://github.com/edx/edx-analytics-dashboard)】
  - Python 2.7.12
  - Django 1.11.15
  - gettext
  - node 8.9.3
  - npm 5.5.1
  - Mysql 5.6
- analytics api 【[github](https://github.com/edx/edx-analytics-data-api)】
  - Django 1.11.15
  - Python 2.7.12
  - Mysql 5.6
- analytics pipeline 【[github](https://github.com/edx/edx-analytics-pipeline)】
  - JDK 8
  - Python 2.7.12
  - Hadoop 2.7.2
  - Hive 2.1.1
  - Sqoop 1.4.6
  - Mysql 5.6

## 二、运行环境

- analytics dashboard 数据展示界面
- analytics_api 提供获取数据api
- pipeline 执行数据分析任务

## 三、相关功能

- analytics dashboard
  - 升级
    - edx版本
      - open-release/ironwood.1
    - 本地版本
      - ironwood【[github](https://github.com/zyingli/edx-analytics-dashboard/tree/ironwood)】
    - 代码路径
      - insights: /edx/app/insights
      - analytics_dashboard: /edx/app/insights/edx_analytics_dashboard 
    - 升级方式
      - 目前未修改相关功能，可直接升级代码
  - 单点登录配置
    - lms服务器： 进入edxapp环境后执行
      ```bash
      /edx/app/edxapp/edx-platform/manage.py lms --setting=aws create_oauth2_client http://insights.eliteu.xyz http://insights.eliteu.xyz/complete/edx-oidc/ confidential --client_name insights --client_id YOUR_OAUTH2_KEY --client_secret secret --trusted
      # http://insights.eliteu.xyz  为数据分析网站url
      # YOUR_OAUTH2_KEY 定义与其他系统不同的 key
      ```
    - 数据分析服务器：修改 /edx/etc/insights.yml 的 SOCIAL_AUTH_EDX_OIDC_KEY 值为上述定义的 YOUR_OAUTH2_KEY
      ```yaml
      SOCIAL_AUTH_EDX_OIDC_KEY: YOUR_OAUTH2_KEY 
      ```

  - web界面功能
    - 地址 http://host:18110/docs/

- analytics api 
  - 升级
    - edx版本
      - open-release/ironwood.1
    - 本地版本
      - ironwood【[github](https://github.com/zyingli/edx-analytics-data-api/tree/ironwood)】
    - 代码路径
      - insights: /edx/app/analytics_api
      - analytics_dashboard: /edx/app/analytics_api/analytics_api
    - 升级方式
      - 目前未修改相关功能，可直接升级代码
  - API 地址 http://host:18100/docs/

- pipeline
  - Insights - pipeline数据分析任务 【[链接](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=233)】

## 四、相关脚本

- analytics dashboard
```bash
# 运行命令
/edx/bin/supervisorctl (start|stop|status) insights
```
- analytics api 
```bash
# 运行命令
/edx/bin/supervisorctl (start|stop|status) analytics_api
```
- analytics pipeline
```bash
# 同步lms的tracking.log到hdfs中
python /edx/app/hadoop/analyize-task/bin/sync_lmslog_to_hdfs.py
# 执行数据分析任务
bash /edx/app/hadoop/analyize-task/bin/run_analyize_task.sh all
```

## 五、发布相关

- [数据分析服务器安装](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=126)
- [定时任务安装](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=196)
- 每天凌晨2点执行一次数据分析任务

## 六、常见问题

- 查看analytics_api、luigid、hdfs、mapreduce等web服务界面需云服务器开放端口

## 七、引用参考

- [edX Analytics Installation](https://openedx.atlassian.net/wiki/spaces/OpenOPS/pages/43385371/edX+Analytics+Installation)
- [edx-analytics-dashboard](https://github.com/edx/edx-analytics-dashboard)
- [edx-analytics-data-api](https://github.com/edx/edx-analytics-data-api)
- [edx-analytics-pipeline](https://github.com/edx/edx-analytics-pipeline)
- [Tasks to Run to Update Insights](https://edx-analytics-pipeline-reference.readthedocs.io/en/latest/running_tasks.html  )