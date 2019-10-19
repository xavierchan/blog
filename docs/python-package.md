---
title: 提交你的第一个python库
toc: true
date: 2019-04-02 19:06:13
tags:
 - python
categories:
 - 笔记
---

### 序言

每个开发者都需要提交自己的第一份开源库，nodejs的提交到npm，java的估计到maven，而咱们python的当然是提交到pypi了，提交你的开源库到库托管网站，是你人生进一个

### 一、创建项目

```python
/example_pkg
  /example_pkg
    __init__.py
```

### 二、创建包文件

```python
/example_pkg
  /example_pkg
    __init__.py
  setup.py
  LICENSE
  README.md
```

### 三、打包上传

```shell
pip install twine # 可以使用setuptools上传，但它上传时账号信息是以明文的形式传输，存在安全问题
python setup.py sdist bdist_wheel # 打包
twine upload dist/* # 上传
```
