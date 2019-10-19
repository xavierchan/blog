---
title: LMS
toc: true
date: 2019-08-20 16:13:09
tags:
categories:
 - openedx
---

## 一、技术栈

- Mysql==5.6.32
- Redis
- memcached
- MongoDB
- Python==2.7.12
- Django==1.11.20
- celery==3.1.25

## 二、运行环境

- 运行用户 - edxapp
- 环境变量 - /edx/app/edxapp/edx-platform/lms.env(auth).json

## 三、相关功能

### 3.1 业务性功能

- 课程证书 - [配置文档](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=79)
- 手机应用配置 - [配置文档](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=72)
- 邮件功能 - [配置文档](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=63)
- 添加CourseTalk小部件&指定允许的注册电子邮件模式&将自定义字段添加到注册页面 - [配置文档](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=263)
- THEMING 主题
  - Site themes 系统主题 - 为对应的Site配置相应的主题名称 => [**使用文档**](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=71)
- 密码校验规则和删除用户功能 - [配置文档](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=252)
- 在Studio和LMS中启用课程证书- [配置文档](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=268)

### 3.2 系统性功能

- OAUTH2
  - Client 客户端

## 四、相关脚本

- 安装lms脚本devstack - [配置文档](http://pms.elitemc.cn/index.php?m=doc&f=view&docID=250)

## 五、发布相关

### 5.1 完整发布流程

```shell
# 1. 切换用户，并切换项目根目录
sudo -H -u edxapp bash
cd /edx/app/edxapp/edx-platform
source /edx/app/edxapp/edxapp_env

# 2. 更新环境变量
# 3. 执行数据库迁移
./manage.py lms migrate --settings=aws

# 4. 多语言翻译
# 5. 静态资源编译
paver update_assets cms --settings=aws

# 6. 重启服务
exit
/edx/bin/supervisorctl restart all
```

## 六、常见问题

## 参考资料

> - [**Ironwood版本edx配置文档**](https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/open-release-ironwood.master/configuration/index.html)
> - [**配置多Site**](https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/open-release-ironwood.master/configuration/sites/index.html)
