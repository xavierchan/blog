---
title: certbot
toc: true
date: 2019-10-08 10:46:36
tags:
categories:
---

```shell
sudo apt-get install nginx
以上过程，等待安装完毕就好。

然后添加 package repository

sudo add-apt-repository ppa:certbot/certbot
这个过程中，等待验证完毕，按下 ENTER 就好。然后更新 apt 源数据：

sudo apt-get update
最后，安装 Certbot 的 Nginx package：

sudo apt-get install python-certbot-nginx
apt update
apt install certbot python-certbot-apache python-certbot-nginx
```


## 参考资料
> - []()
> - []()
