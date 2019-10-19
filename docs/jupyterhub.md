---
title: jupyterhub
toc: true
date: 2019-09-27 15:28:20
tags:
categories:
---

### requirements - 准备

- python 3.5+
- jupyterhub 0.8.*
- oauthlib 2.*.*

### 一、Docker 运行 JupyterHub
0.8.1
```shell
docker run -d -p 8300:8000 --name jupyterhub jupyterhub/jupyterhub:1.0.0 jupyterhub && docker exec -it jupyterhub bash
apt update && apt install -y vim && pip install jupyterhub-ltiauthenticator tornado==5.1.1 notebook==5.6.0 && jupyterhub --generate-config
```

### 二、更新 jupyterhub_config.py 配置文件

```python
# 需要配置 headers ，否则无法通过 frame 集成
c.JupyterHub.tornado_settings = {
    'headers': {
        'Content-Security-Policy': "frame-ancestors *"
  }
}
# 修改认证器
from IPython.utils.localinterfaces import public_ips
c.JupyterHub.hub_ip = public_ips()[0]
c.Authenticator.admin_users = {'user'}
c.JupyterHub.api_tokens = {
    'f05ebd3853894ecccfc8c8b4d139618a' : 'user',
}
c.JupyterHub.allow_named_servers = True
c.LocalAuthenticator.create_system_users = True
from ltiauthenticator import LTIAuthenticator
from jupyterhub.auth import LocalAuthenticator
class LocalLtiAuthenticator(LocalAuthenticator, LTIAuthenticator):
    pass
c.JupyterHub.authenticator_class = 'ltiauthenticator.LTIAuthenticator'
c.JupyterHub.authenticator_class = LocalLtiAuthenticator
c.LTIAuthenticator.consumers = {
    "438d973eb17345164f54b243a58db2454c635d3b2ddbdae0eedc10f1d324367f": "99a4a8cc1209492c779bb1f951fcd5959fa6824e2b7cb9d00e924a81da568e3c"
}
c.NotebookApp.allow_remote_access = True
```

需要降级，否则无法
pip install tornado==4.5.3

## 参考资料
