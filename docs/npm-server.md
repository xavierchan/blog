---
title: 私有npm库搭建
toc: true
date: 2019-04-02 19:15:42
tags:
 - npm
categories:
 - 解决方案
---
## 1. 需求
项目不断迭代发展，除了完成刚需业务功能，还需要重构优化、或者是定制私有代码片段。
在这种情况下，我们希望在使用的时候能方便地一个指令完成安装，又不希望非公司人员使用到，某种程度上限制或对企业项目资产进行保护，
这时候就需要建立企业自己的私有仓库(npm或者pip)

## 2. 开源项目选择
|参数|cnpm|sinopia(verdaccio)|
|:---:|:---:|:---:|
|star|1.9k|4.5k(2.4k)|
|系统支持|非windows|全系统|
|安装|复杂|简单|
|配置|较多，适合个性化需求较多的|较少|
|配置——修改默认镜像|不支持|支持|
|存储|mysql|文件格式，直观|
|服务托管|默认后台运行|pm2, doker, forever|
|文档资料|较多|较少|
cnpm(company npm)支持企业私有仓库搭建，但以上对比下你会发现，对于小团队来说，sinopia自建npm服务器是个不错的选择，轻量简单，不过自15年开始sinopia就已经停止维护了，不过幸好有新的团队对他进行了延续，那就是[verdaccio](http://www.verdaccio.org)([github](https://github.com/verdaccio/verdaccio))

## 3. verdaccio简介
verdaccio是个轻量的私有npm服务器应用，无缝连接npm所有api，使用了nodejs+react技术实现，自带web应用(默认端口4873)，web ui提供了仿npmjs的界面，具有包列表、详情、登录等简易功能

## 4. 搭建流程
1. 一键安装
```shell
npm install -g verdaccio                      # 安装verdaccio
```
2. supervisor托管应用，域名解析配置(以下是运行指令，具体配置请自行查询)
```shell
verdaccio -c $config_path
```
3. 使用
```shell
npm adduser --registry $registry_path   # 注册用户
npm login --registry $registry_path     # 登录用户
npm publish --registry $registry_path   # 发布包
npm unpublish $package@$version        # 删除某版本发布包

```

## 5. 使用说明
### 5.1 nrm
npm镜像地址管理工具，使用nrm工具方便切换仓库地址，便于维护和减少指令参数的输入
```shell
nrm ls                            # 查看列表
nrm add $alias $registry_path   # 添加仓库地址
nrm use $alias                   # 切换到仓库
nrm del $alias                  # 删除仓库
```

### 5.2 配置说明

```html
cd /home//.config/verdaccio # 进入默认配置目录
verdaccio
  ├─ config.yaml                         # 配置文件
  ├─ htpasswd                            # 认证信息
  ├─ storage                             # 包存储目录
       ├─ .sinopia-db.json               # 包数据列表
       ├─ robots.txt/                    # 暂时不明
       ├─ test-eliteu/                   # 某发布包名称
            ├─ package.json              # 包信息详情
            ├─ test-eliteu-1.1.0.tgz     # 每个版本一个压缩包
            ├─ test-eliteu-1.2.0.tgz
```
