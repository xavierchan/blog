---
title: supervisor
toc: true
date: 2019-04-02 19:21:52
tags:
categories:
 - 笔记
---
### 安装
pip install supervisor

### 生成默认配置文件
echo_supervisord_conf > /etc/supervisord.conf

#### 三、常用指令
```
> supervisord -c /etc/supervisord.conf # 配置文件，守护进程形式启动服务
> supervisorctl shutdown # 关闭服务
> supervisorctl # 打开命令行
> supervisorctl update # 更新配置
> supervisorctl reload # 重启所以程序
> supervisorctl start $program # 启动某个程序
> supervisorctl restart $program # 重启某个程序
> supervisorctl stop $program # 停止某个程序
supervisorctl -uuser -p123 shutdown # 认证模式操作
```

#### 四、服务配置demo
```
[program:blog]                          ; 是应用程序的唯一标识，不能重复
directory = /Users/xavierchan/Documents/xavier/xavierchan.github.io
command = /usr/local/bin/hexo s -d ; 启动命令
autostart = true                        ; 在 supervisord 启动的时候也自动启动
startsecs = 5                           ; 启动 5 秒后没有异常退出，就当作已经正常启动了
autorestart = true                      ; 程序异常退出后自动重启
startretries = 3                        ; 启动失败自动重试次数，默认是 3
redirect_stderr = true                  ; 把 stderr 重定向到 stdout，默认 false
stdout_logfile_maxbytes = 20MB
stdout_logfile_backups = 20
stdout_logfile = /var/log/supervisor/blog.log   ; stdout 日志文件，注意：要确保目录已经建立并且可以访问（写权限）
```


## 参考资料
> - []()
> - []()
