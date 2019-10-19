---
title: Memcached
toc: true
date: 2019-04-02 19:11:04
tags:
 - 缓存
categories:
 - 数据库
---
```python
$ mc.get_stats('items') # 获取所有键值对
```
1、启动Memcache 常用参数

复制代码
-p <num>      设置TCP端口号(默认设置为: 11211)
-U <num>      UDP监听端口(默认: 11211, 0 时关闭) 
-l <ip_addr>  绑定地址(默认:所有都允许,无论内外网或者本机更换IP，有安全隐患，若设置为127.0.0.1就只能本机访问)
-c <num>      max simultaneous connections (default: 1024)
-d            以daemon方式运行
-u <username> 绑定使用指定用于运行进程<username>
-m <num>      允许最大内存用量，单位M (默认: 64 MB)
-P <file>     将PID写入文件<file>，这样可以使得后边进行快速进程终止, 需要与-d 一起使用
复制代码
复制代码
更多可以使用者 memcached -h
在linux下：./usr/local/bin/memcached -d -u root  -l 192.168.1.197 -m 2048 -p 12121
在window下：d:\App_Serv\memcached\memcached.exe -d RunService -l 127.0.0.1 -p 11211 -m 500
在windows下注册为服务后运行：
sc.exe create Memcached_srv binpath= “d:\App_Serv\memcached\memcached.exe -d RunService -p 11211 -m 500″start= auto
net start Memcached
复制代码

2、连接和退出
```shell
telnet 127.0.0.1 11211
quit
```

Memcached 查询stats及各项状态解释
一、两个最常用状态查询（掌握第一个就完全OK了）

      1）查看状态：printf “stats\r\n” |nc 127.0.0.1 11211
      2）模拟top命令查看状态：watch “echo stats” |nc 127.0.0.1 11211

二、各种stats中文解释。但工作中最常关注的只有四个。

      STAT get_hits 1（序号，并不是结果，如下）

      STAT get_misses 2

      STAT curr_items 3

      STAT total_items 4

  各种stats中文解释如下：

        

1.  pid: memcached服务进程的进程ID

2.  uptime: memcached服务从启动到当前所经过的时间，单位是秒。

3.  time: memcached服务器所在主机当前系统的时间，单位是秒。

4.  version: memcached组件的版本。

5.  pointer_size：服务器所在主机操作系统的指针大小，一般为32或64.

6.  curr_items：表示当前缓存中存放的所有缓存对象的数量。不包括目前已经从缓存中删除的对象。

7.  total_items：表示从memcached服务启动到当前时间，系统存储过的所有对象的数量，包括目前已经从缓存中删除的对象。

8.  bytes：表示系统存储缓存对象所使用的存储空间，单位为字节。

9.  curr_connections：表示当前系统打开的连接数。

10. total_connections：表示从memcached服务启动到当前时间，系统打开过的连接的总数。

11. connection_structures：表示从memcached服务启动到当前时间，被服务器分配的连接结构的数量，这个解释是协议文档给的，具体什么意思，我目前还没搞明白。

12. cmd_get：累积获取数据的数量

13. cmd_set：累积保存数据的树立数量

14. get_hits：表示获取数据成功的次数。

15. get_misses：表示获取数据失败的次数。

16. evictions：为了给新的数据项目释放空间，从缓存移除的缓存对象的数目。比如超过缓存大小时根据LRU算法移除的对象，以及过期的对象。

17. bytes_read：memcached服务器从网络读取的总的字节数。

18. bytes_written：memcached服务器发送到网络的总的字节数。

19. limit_maxbytes：memcached服务缓存允许使用的最大字节数。这里为67108864字节，也就是是64M.与我们启动memcached服务设置的大小一致。

20. threads：被请求的工作线程的总数量。这个解释是协议文档给的。




## 参考资料
> - []()
> - []()
