---
title: 如何在Open edX中集成cas
toc: true
date: 2019-04-02 19:03:07
tags:
 - 笔记
categories:
 - openedx
---
### 序言
“Open edX是个庞大而复杂的系统”，这句话估计业内的人都听得不少了，所以对这样的一个系统来说，SSO是个刚需。笔者最近由于工作原因，需要在这块躺下坑，为了造福后人，决定把这踩坑过程记录下。

### 一、需求
公司的产品 **[E-ducation](http://www.e-ducation.cn)** 是提供edx系统的SaaS服务平台，客户只需5分钟的注册配置，就能拥有全套的edx学习系统。
但多个系统之间由于域名原因，登录状态相互隔离了，使用一个平台需要来回登录，而对于用户来说这是个麻烦事，因此为了给客户提供良好便捷的用户体验，我们决定实现SSO，打通系统之间的登录问题。

### 二、思路
#### 2.1 SSO技术
对于SSO实现的手段，笔者了解的jwt和cas都可以实现，但基于跨域问题，只能采取cas，而且本身edx是已经提供cas的客户端配置。
#### 2.2 edx项目
从技术层面来分析edx-platform，所有系统的操作都是同一个数据库
#### 2.3 实现方式
CAS，分为Client和Server，据我的认识，Server作为认证服务端，其他的均为客户端，所有客户端登录先判定服务端是否登录，已登录的话就根据ticket获取登录的用户信息，未登录的就重定向到服务端进行登录。

通过配置的话，我们宏观上他的表现是很简单的，但内在你集成的库替你做了很多事情，一些典型的过程我已经形成时序图在下面给大家演示。

流程上是比较繁琐的，笔者理解能力不算很强，下面举个买门票的栗子形象说明下。
- 有两家游乐园(CA、CB)都加入了一个联盟组织(S)，大家达成了协议，游客买票都需要到S的实名制系统核查身份才能分发门票

#### 2.4 集成时遇到的问题
1. 统一登出暂未研究出结果，需要自行拓展
2. lms做了域名和企业的隔离，cas需要多做一层企业用户检验，否则修改url会以其他登录的用户身份登录进来
3. 未登录页面统一处理
3. 入口统一处理，目前个人版、企业版lms入口有改动，个人版还是页面弹窗形式的
4. 只支持username登录，而当前我们使用了手机和邮箱的

#### 1 用户访问应用A
```
sequenceDiagram
Brower->>Client A: 访问受限资源
Client A->>Client A: 检验到未登录
Client A->> Cas Server: 重定向 cas/login?service=a url
Cas Server->> Cas Server: 检测到全局未登录
Cas Server->> Brower: 返回登录页面
Brower->> Cas Server: 输入账号密码，登录
Cas Server->> Cas Server: 验证通过，登录成功，保存session
Cas Server->> Client A: 重定向 cas/login?ticket=xxx
Client A->> Client A: 拦截登录请求，获取ticket
Client A->> Cas Server: 重定向 proxyVa?ticket=xxx
Cas Server->> Client A: 验证通过
Client A->> Client A: 登录成功，保存session
Client A->>Brower: 浏览器保存session
Brower->>Client A: 访问受限资源
```

#### 2 用户访问应用B
```
sequenceDiagram
Brower->>Client B: 访问受限资源
Client B->>Client B: 检验到未登录
Client B->> Cas Server: 重定向 cas/login?service=b url
Cas Server->> Cas Server: 检测到全局已登录
Cas Server->> Client B: 重定向 cas/login?ticket=xxx
Client B->> Client B: 拦截登录请求，获取ticket
Client B->> Cas Server: 重定向 proxyVa?ticket=xxx
Cas Server->> Client B: 验证通过
Client B->> Client B: 登录成功，保存session
Client B->>Brower: 浏览器保存session
Brower->>Client B: 访问受限资源
```

#### 3 用户登出应用A




## 参考资料
> - []()
> - []()
