---
title: k8s
toc: true
date: 2019-04-10 14:20:57
tags:
categories:
 - 容器技术
---
#### 常用指令
#### 管理多个集群
```shell
cd ~/.kube
KUBECONFIG=第一个配置文件:第二个配置文件 kubectl config view --flatten > config # 合并配置，并写入config（注意！！！建议先备份配置）
kubectl config view # 查看配置，会发现阿里云集群名字特长，根据自己偏好，修改集群的context的name
kubectl config current-context # 查看当前上下文配置名
kubectl config use-context $context-name # 切换上下文配置名
```
#### get
```shell
kubectl get ns # 获取所有namespace
kubectl get node # 获取所有节点
kubectl -n {$nameSpace} get pods # 在指定的namespace下获取资源
kubectl get {$sourceType} --all-namespaces
```

## K8S常见问题
### pv或相关资源无法删除
一般删除步骤为：先删pod再删pvc最后删pv
kubectl delete po mongodb-77d675597b-79m2l -n openedx-xavierchan12 --force --grace-period=0
一定要带上namespace，否则删除不成功


## 参考资料
> [kubectl连接多个集群](https://blog.csdn.net/wiselyman/article/details/84917063)
> - []()
> - []()
