---
title: htop
date: 2017-12-31 16:47:48
tags:
---
#### 一、简介
This is htop, an interactive process viewer for Linux. It is a text-mode application (for console or X terminals) and requires ncurses.


#### 二、特性

#### 三、安装
```
> yum install htop # yum安装
```

Shortcut Key|Function Key|Description|中文说明
:-:|:-:|:-:|:-:|
h, ?|F1|Invoke htop Help|查看htop使用说明
S|F2|Htop Setup Menu|htop 设定
/|F3|Search for a Process|搜索进程
\|F4|Incremental process filtering|增量进程过滤器
t|F5|Tree View|显示树形结构
<, >|F6|Sort by a column|选择排序方式
[|F7|Nice - (change priority)|可减少nice值，这样就可以提高对应进程的优先级
]|F8|Nice + (change priority)|可增加nice值，这样就可以降低对应进程的优先级
k|F9|Kill a Process|可对进程传递信号
q|F10|Quit htop|结束htop