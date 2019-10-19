---
title: ELK stack
date: 2018-03-12 17:25:17
tags:
categories:
---

## 前言
### Elasticsearch 搜索引擎
Elasticsearch是个开源分布式搜索引擎，它的特点有：分布式，零配置，自动发现，索引自动分片，索引副本机制，restful风格接口，多数据源，自动搜索负载等。

### Logstash 日志收集工具
Logstash是一个完全开源的工具，他可以对你的日志进行收集、过滤，并将其存储供以后使用（如，搜索）。

### Kibana 日志可视化工具
Kibana也是一个开源和免费的工具，Kibana可以为 Logstash 和 ElasticSearch 提供的日志分析友好的 Web 界面，可以帮助您汇总、分析和搜索重要数据日志。


## 步骤
0. 安装JDK
```shell
$ wget http://download.oracle.com/otn-pub/java/jdk/8u161-b12/2f38c3b165be4555a1fa6e98c45e0808/jdk-8u161-linux-x64.tar.gz
```

1. 下载软件源码包
```shell
$ wget https://artifacts.elastic.co/downloads/logstash/logstash-6.2.2.tar.gz
```
无需安装，直接使用

2. 创建配置文件
```conf
input { stdin { } }
output {
  elasticsearch { hosts => ["localhost:9200"] }
  stdout { codec => rubydebug }
}
```

3. 运行logstash
```shell
$ bin/logstash -f logstash-simple.conf
```

### 常见问题
1. Java HotSpot(TM) 64-Bit Server VM warning: INFO: os::commit_memory(0x0000000085330000, 2060255232, 0) failed; error='Cannot allocate memory' (errno=12)
logstash 使用jvm，默认配置是1g的内存，需要修改大小
位置：config/jvm.options  (Xms1g)

2. Elasticsearch不能用root启动
addgroup elsearch
adduser elsearch -g elsearch -p elsearch
chown -R elsearch:elsearch [elsearch]

3. ERROR: bootstrap checks failed
max file descriptors [4096] for elasticsearch process likely too low, increase to at least [65536]
max number of threads [1024] for user [elsearch] likely too low, increase to at least [2048]
根据提示，修改限制
# vi /etc/security/limits.conf      #永久设置
elsearch soft nofile 65536
elsearch hard nofile 65536
elsearch soft nproc 2048
elsearch hard nproc 2048

4. transport: dial unix /var/run/docker/containerd/docker-containerd.sock: connect: connection refuse
解决办法：service docker restart 重启docker


