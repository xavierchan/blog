---
title: react学习之dva
date: 2018-01-09 14:15:54
tags:
categories:
---

折腾一番之后，总结了使用dva开发前端项目要走的基本流程，如果要开发更复杂酷炫的应用，在这上面继续扩展。
1. 在routes文件夹新建个路由，其实我一直觉得“路由”这个词很别扭，用“容器组件”更恰当一些。
2. 在components文件夹定义UI组件，容器组件就是靠这些UI组件组合起来的。
3. 在models文件夹定义model文件，model文件负责管理一个容器组件的模型，包含同步更新 state 的 reducers，处理异步逻辑（主要是ajax请求）的 effects。
4. 最后，在容器组件中，把model和component串联起来，以antd官方的demo为例

