---
title: jupyter
toc: true
date: 2019-09-06 10:07:31
tags:
categories:
---

### 前言

[Jupyter](https://jupyter.org)

### FAQ

1. UnicodeDecodeError: 'ascii' codec can't decode byte 0xe5 in position 4: ordinal not in range(128)
解决：LANG=zn jupyter-notebook

2. 无法创建Python3环境
解决：
sudo pip3 install --upgrade pip
pip3 install ipykernel
python3 -m ipykernel install
