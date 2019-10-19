---
title: helm
toc: true
date: 2019-09-06 14:38:41
tags:
categories:
---

```shell
helm reset [-f] # 删除tiller
helm init # 初始化，重新部署tiller

# 1. client 和 server 版本要一致，否则容易会有异常
# 2. 需要先创建 --service-account tiller，否则后面初始化 tiller server 会不成功，找不到这个账号，详情可以参考[helm rbac](https://helm.sh/docs/rbac/#role-based-access-control)

brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/ee94af74778e48ae103a9fb080e26a6a2f62d32c/Formula/kubernetes-helm.rb
helm init --service-account tiller --history-max 200 --upgrade -i registry.cn-hangzhou.aliyuncs.com/google_containers/tiller:v2.11.0 --stable-repo-url https://kubernetes.oss-cn-hangzhou.aliyuncs.com/charts

helm version # 检查版本安装是否正常
helm list # 检查helm权限是否正常
```
