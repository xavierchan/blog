---
title: 开启SAML功能
toc: true
date: 2019-04-15 16:12:22
tags:
 - openedx
 - saml
categories:
 - openedx
---
### 1 服务端(LMS)开启SAML功能
#### 1.1 编辑lms.env.json
```json
"FEATURES" : {
    "ENABLE_COMBINED_LOGIN_REGISTRATION": true,
    "ENABLE_THIRD_PARTY_AUTH": true
},
"THIRD_PARTY_AUTH_BACKENDS": [
    "third_party_auth.saml.SAMLAuthBackend"
]
```
#### 1.2 为SP生成秘钥对，并配置到环境变量lms.auth.json中

##### 1.2.1 生成keys pair
```shell
openssl req -new -x509 -days 3652 -nodes -out saml.crt -keyout saml.key
```

#### 1.2.2 更新到环境变量(去掉头尾注释)
```json
"SOCIAL_AUTH_SAML_SP_PUBLIC_CERT": "",
"SOCIAL_AUTH_SAML_SP_PRIVATE_KEY": "",
```

#### 1.3. 在Third_Party_Auth中，添加SAML Configuration
edx中不可删除，变更的话只会增多一条记录

检验IDP元数据是否获取成功
在Third_Party_Auth中，添加SAML Provider Data，is_valid 为绿色，则idp元数据获取成功
- Entity id 为元数据ID
- Metadata source 为元数据地址
- SSO URL idp单点登录重定向地址
- public key sp的公钥

### 2 edx实例为企业添加SAML配置
#### 2.1 SAML集成资料提交
1. 域名
2. 按钮显示名称
3. 元数据地址(eg. https://saml.xavierit.cn/idp/metadata/)

#### 2.2 SP为企业创建SAML配置
1. 创建(或更新) **Site**
2. 创建并配置(或更新) **Site configurations**
3. 创建(或更新) **SAML Configuration**
4. 创建(或更新) **Provider Configuration (SAML IdP)**

#### IDP集成步骤
1. 访问 domain/auth/saml/metadata.xml ，检查自己的SP元数据是否有问题；
2. 检查IDP的元数据是否有问题；
3. 配置SP相关信息；


#### 注意
?tpa_hint

## 参考资料
> - [openedx](https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/latest/configuration/tpa/tpa_integrate_open/tpa_SAML_IdP.html?highlight=saml)
> - [jenyzhang blog](https://blog.csdn.net/jenyzhang/article/details/52957529)
