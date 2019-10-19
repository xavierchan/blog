---
title: vim使用笔记
date: 2018-01-22 09:21:38
tags:
- vim
categories:
- 有用功
---

### 常用指令
yy 拷贝一行
dd 剪切一行
p 粘贴
/string 搜索string
?string 搜索string
o 新建一行
0 行首
$ 行尾

### 一、光标移动指令
w: 光标移动到下一个单词的词首；注：对于中文，连续的多个汉字作为一个word。
e: 光标移动到下一个单词的词尾；
b: 向前移动光标，移动到前一个单词的词首

### 替换
%s/a/b/g 用b替换所有的a

### 二、翻页指令
ctrl + f # 向下翻页
ctrl + b # 向上翻页


### 三、分屏指令

1. 查组用户 GET
2. 分配组 POST

'2018-01-22 15:30:00'
'NAME': 'eliteu_support_system',
  7         'USER': 'eliteu_support',
  8         'PASSWORD': 'FG34r2rfrf3',
  9         'HOST': 'localhost',

### vim升级8.0尝鲜
yum install ncurses-devel
wget https://github.com/vim/vim/archive/master.zip
unzip master.zip
cd vim-master
cd src/
./configure
make
sudo make install
vim

/var/log/nginx/access.log