---
title: elasticsearch-note
date: 2018-05-13 20:02:07
tags:
- ELK
categories:
---

docker run -d --name elasticsearch --restart=always \
-p 9200:9200 -p 9300:9300 \
-v /root/docker/elasticsearch/config:/usr/share/elasticsearch/config \
-v /root/docker/elasticsearch/data:/usr/share/elasticsearch/data \
elasticsearch:5.6.9

### 常用搜索

```es
status:active # 准确搜索

```

[query string 语法](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html#query-string-syntax)
