---
title: Kibana
date: 2018-05-11 15:52:37
tags:
categories:
---

docker run -d --name kibana -p 5601:5601 -e "ELASTICSEARCH_URL=http://localhost:9200" --network host kibana:5.6.9
docker run -d --name kibana -e ELASTICSEARCH_URL=http://some-elasticsearch:9200 -p 5601:5601 kibana:5.6.9
