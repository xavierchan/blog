---
title: Logstash
toc: true
date: 2019-04-02 19:20:28
tags:
 - elk
categories:
 - 笔记
---
-logstash配置文件一般分为两类
1. 管道配置文件(Pipeline Configuration Files)
管道配置文件相当于 ***/etc/logstash/conf.d*** 或者 ***/etc/logstash.d/*** 目录下的 *.conf 文件
他的作用是配置 输入 过滤 输出
2. 配置文件(Settings Files)
而settings配置文件，是对服务的基本配置


配置文件运行服务
bin/logstash -f logstash.conf

docker run -d --restart=always --name logstash --network host \
-v /etc/logstash/conf.d/:/usr/share/logstash/pipeline/ \
-v /var/log:/var/log \
logstash:5.6.9

/root/docker/config/logstash

–config 或 -f
意即文件。真实运用中，我们会写很长的配置，甚至可能超过 shell 所能支持的 1024 个字符长度。所以我们必把配置固化到文件里，然后通过 bin/logstash -f agent.conf 这样的形式来运行。

此外，logstash 还提供一个方便我们规划和书写配置的小功能。你可以直接用 bin/logstash -f /etc/logstash.d/ 来运行。logstash 会自动读取 /etc/logstash.d/ 目录下所有 *.conf 的文本文件，然后在自己内存里拼接成一个完整的大配置文件，再去执行。
