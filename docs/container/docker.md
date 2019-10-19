---
title: docker
date: 2017-12-31 23:24:57
tags:
categories:
- 容器技术
---

### 常用命令

```shell
docker version # 可查看docker版本及是否运行
docker info # docker所有信息
docker image ls # 镜像列表
docker container ls # 容器列表
docker search 镜像名字
$ docker login [-u <用户名> -p <密码>] # 登录
$ docker logout # 退出登录
$ docker tag redis:last redis::4.0.7
$ docker load < redis.tar # 载入镜像
$ docker tag {id} repo:tag # 修改镜像信息
```

### 通过Dockerfile定义容器

1. 配置文件

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```
1. 创建容器
```bash
$ docker build -t friendlyhello . # 根据当前目录下的配合文件，创建名为“friendlyhello”的镜像
$ docker run -d -p 4000:80 friendlyhello # 运行friendlyhello镜像(-d 守护进程运行)
```

#### 查看控制台输出
```bash
sudo docker logs -f -t --tail 行数 容器名
docker start -i eliteu-live # 连接进服务器容器内
```
