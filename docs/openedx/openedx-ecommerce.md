---
title: E-commerce
toc: true
date: 2019-04-09 00:26:30
tags:
categories:
 - openedx
---

edX native install 安装的环境启用 ecommerce 需要

在 lms 的 admin 后台添加 oauth2 client

修改 ecommerce 配置

修改 lms 配置

修改配置后重启 ecommerce 和 lms





### 添加 oauth2 client



登录 LMS admin 后台，创建 ecommerce 的 oauth2 client，如果 client 已存在，则修改

- URL 需要匹配 commerce 的域名

- client id 和 client secret 会自动生成，也可以自己设置。后面修改 ecommerce 配置的时候会用到





将创建好的 Oauth2 client 添加到 trusted client



Ps：如果没有超级管理员账号可以修改 staff 账号的权限，修改后账号密码为 staff/edx

> /edx/bin/python.edxapp /edx/bin/manage.edxapp lms manage_user staff staff@example.com --staff --superuser --settings=aws


### 修改 ecommerce 配置



native install 的 ecommerce 跑的是 production.py 的配置

可修改的配置文件是 /edx/etc/ecommerce.yml

edX 使用 Ansible 创建和更新配置文件，我们可以自己修改 ecommerce.yml

---

# This file is created and updated by ansible, edit at your peril

...

ECOMMERCE_URL_ROOT: http://ecommerce.eliteu.xyz

EDX_API_KEY: PUT_YOUR_API_KEY_HERE

EDX_DRF_EXTENSIONS:

    OAUTH2_USER_INFO_URL: http://www.eliteu.xyz/oauth2/user_info

ENABLE_COMPREHENSIVE_THEMING: false

ENTERPRISE_SERVICE_URL: http://127.0.0.1:8000/enterprise/

EXTRA_APPS: []

JWT_AUTH:

    JWT_ALGORITHM: HS256

    JWT_DECODE_HANDLER: ecommerce.extensions.api.handlers.jwt_decode_handler

    JWT_ISSUERS:

    - http://www.eliteu.xyz/oauth2

    - ecommerce_worker

    JWT_LEEWAY: 1

    JWT_SECRET_KEY: SET-ME-PLEASE

    JWT_SECRET_KEYS:

    - SET-ME-PLEASE

    JWT_VERIFY_EXPIRATION: true

...

PLATFORM_NAME: Your Platform Name Here

SECRET_KEY: FMU41vax6gDlp33EuDJ47pRsZUMggdPdaWPigA4IoQVoC0Wn0aM4li7EnQCgPGL98U8hbZPetrRxWWpso5bgMl6jUqiVlCtmfQxb

SESSION_COOKIE_SECURE: false

SESSION_EXPIRE_AT_BROWSER_CLOSE: false

SOCIAL_AUTH_EDX_OIDC_ID_TOKEN_DECRYPTION_KEY: ecommerce-secret

SOCIAL_AUTH_EDX_OIDC_ISSUER: http://www.eliteu.xyz/oauth2

SOCIAL_AUTH_EDX_OIDC_KEY: ecommerce-key

SOCIAL_AUTH_EDX_OIDC_LOGOUT_URL: http://www.eliteu.xyz/logout

SOCIAL_AUTH_EDX_OIDC_PUBLIC_URL_ROOT: http://www.eliteu.xyz/oauth2

SOCIAL_AUTH_EDX_OIDC_SECRET: ecommerce-secret

SOCIAL_AUTH_EDX_OIDC_URL_ROOT: http://www.eliteu.xyz/oauth2

SOCIAL_AUTH_REDIRECT_IS_HTTPS: false

...







### 修改 lms 的配置



/edx/app/edxapp/lms.env.json

    "ECOMMERCE_API_URL": "http://ecommerce.eliteu.xyz/api/v2",

    "ECOMMERCE_PUBLIC_URL_ROOT": "http://ecommerce.eliteu.xyz",

    ...

    "FEATURES": {

        "AUTH_USE_OPENID_PROVIDER": true,

        "ENABLE_OAUTH2_PROVIDER": true,

        ...

        "ENABLE_THIRD_PARTY_AUTH": true,

    },

    "JWT_AUTH": {

        "JWT_AUDIENCE": "SET-ME-PLEASE",

        "JWT_ISSUER": "http://www.eliteu.xyz/oauth2",

        "JWT_ISSUERS": [

            {

                "AUDIENCE": "SET-ME-PLEASE",

                "ISSUER": "http://www.eliteu.xyz/oauth2",

                "SECRET_KEY": "SET-ME-PLEASE"

            }

        ],

        "JWT_SECRET_KEY": "SET-ME-PLEASE"

    },

    "JWT_EXPIRATION": 30,

    "JWT_EXPIRED_PRIVATE_SIGNING_KEYS": [],

    "JWT_ISSUER": "http://www.eliteu.xyz/oauth2",

    "JWT_PRIVATE_SIGNING_KEY": null,

    ...

    "OAUTH_OIDC_ISSUER": "http://www.eliteu.xyz/oauth2",

    ... 





/edx/app/edxapp/lms.auth.json

"ECOMMERCE_API_SIGNING_KEY": "insecure-secret-key" // Must match the E-Commerce JWT_SECRET_KEY setting

"EDX_API_KEY": "PUT_YOUR_API_KEY_HERE" // Must match the E-Commerce EDX_API_KEY setting 





然后要在https://ecommerce.elitemba.cn/admin/core/siteconfiguration/里面，把对应的OAuth settings设置好（注意修改对应的域名地址）:


{

  "SOCIAL_AUTH_EDX_OIDC_ID_TOKEN_DECRYPTION_KEY":"ecommerce-secret",

  "SOCIAL_AUTH_EDX_OIDC_URL_ROOT":"https://www.elitemba.cn/oauth2",

  "SOCIAL_AUTH_EDX_OIDC_ISSUERS":[

    "https://www.elitemba.cn"

  ],

  "SOCIAL_AUTH_EDX_OIDC_KEY":"ecommerce-key",

  "SOCIAL_AUTH_EDX_OIDC_SECRET":"ecommerce-secret"

}




### 重启 ecmmerce 和 LMS

sudo /edx/bin/supervisorctl restart ecommerce
sudo /edx/bin/supervisorctl restart lms




## 参考资料
> - []()
> - []()
