---
title: hexo，零成本快速搭建个人博客
date: 2018-01-03 12:20:05
tags:
- hexo
- blog
categories:
- 笔记
---

### 序言
hexo是一个简单快速的博客框架，通过命令行生成纯静态的博客页面

### 一、安装cli工具
``` bash
$ npm install hexo-cli -g
```

### 二、创建博客项目
```bash
$ hexo init <proj>  # 创建项目
$ cd <proj>         # 进入项目根目录
$ npm install       # 安装依赖
```

执行完以上指令后，便可得到hexo的博客项目，项目的基本结构如下，对应是功能就不啰嗦描述，请自行浏览官方文档：
```
.
├─ _config.yml
├─ package.json
├─ scaffolds
├─ source
|   ├─ _drafts
|   └─ _posts
└─ themes
```

### 三、主题
用hexo搭建个人博客，很大原因是因为他的可定制性比较高，一个号的博客，第一首先要有个赏心悦目的主题，才能好好阅读观看
1.  安装主题文件
``` bash
$ git clone https://github.com/tufu9441/maupassant-hexo.git themes/maupassant
$ npm install hexo-renderer-pug --save
$ npm install hexo-renderer-sass --save
```
2. 主题配置修改
通过修改 _config.yml 配置文件中，theme 配置来变更使用的主题，主题的名称对应 themes 目录下的安装的主题名
``` bash
$ hexo generate # 生成静态文件
```