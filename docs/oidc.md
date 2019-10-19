---
title: oidc
toc: true
date: 2019-05-23 22:21:49
tags:
categories:
---
OIDC是OpenID Connect的简称，OIDC=(Identity, Authentication) + OAuth 2.0。它在OAuth2上构建了一个身份层，是一个基于OAuth2协议的身份认证标准协议。我们都知道OAuth2是一个授权协议，它无法提供完善的身份认证功能（关于这一点请参考[认证授权] 3.基于OAuth2的认证（译）），OIDC使用OAuth2的授权服务器来为第三方客户端提供用户的身份认证，并把对应的身份认证信息传递给客户端，且可以适用于各种类型的客户端（比如服务端应用，移动APP，JS应用），且完全兼容OAuth2，也就是说你搭建了一个OIDC的服务后，也可以当作一个OAuth2的服务来用。




## 参考资料
> - [oidc 官网](https://openid.net/connect/)
> - []()
