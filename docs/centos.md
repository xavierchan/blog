---
title: centos
toc: true
date: 2019-09-27 09:31:24
tags:
categories:
---

使用yum提示Error: rpmdb open failed
在centos系统上，在使用yum命令安装软件包时候报错：

rpmdb: Thread/process 6539/140448388269824 failed: Thread died in Berkeley DB library
error: db3 error(-30974) from dbenv->failchk: DB_RUNRECOVERY: Fatal error, run database recovery
error: cannot open Packages index using db3 -  (-30974)
error: cannot open Packages database in /var/lib/rpm
CRITICAL:yum.main:
原因是RPM数据库被破坏

重建数据库后恢复正常：

cd /var/lib/rpm/
for i in `ls | grep 'db.'`;do mv $i $i.bak;done
rpm --rebuilddb
yum clean all


## 参考资料
> - []()
> - []()
