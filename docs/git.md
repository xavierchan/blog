---
title: Git
date: 2018-01-18 22:22:14
categories:
- 笔记
---

### 一、常用操作

```shell
git init                              # 项目根目录下
git remote add origin {resp}          # 增加远端仓库
git reset <file\_name>                # 取消暂存
```

### 二、配置管理

```shell
git config --local --unset credential.helper    # 删除配置
git config --global --unset credential.helper
git config --system --unset credential.helper
git config core.ignorecase false                # 取消大小写忽略的设置
```

### 三、工作流管理

### 四、标签管理

标签管理，即软件的版本标注，分为 ***轻量标签*** 和 ***附注标签***。
一般我们使用 ***附注标签*** ，因为它是一个完整的对象，包含打标签者的名字、电子邮件地址、日期时间。

```shell
git tag                           # 查看所有的tag
git tag -l 'v1.4.2.*'             # 查指定版本
git show v1.4                     # 查看版本详情
git tag -a tagName -m "remark"    # 创建本地tag
git tag -d tagName                # 删除本地tag
git push origin tagName           # tag推到远端仓库
git push origin –-detele tagName  # 删除远端仓库tag
```
