---
title: python编码问题
date: 2018-04-13 10:33:18
tags:
categories:
---

MySQL-python安装预装
yum install mysql-devel
yum install python-devel

2.使用decode：
str1 = '\u4f60\u597d'
print str1.decode('unicode_escape')
你好
unicodestr.decode('unicode_escape')  # 将转义字符\u读取出来

# ’\u’开头就基本表明是跟unicode编码相关的，“\u”后的16进制字符串是相应汉字的utf-16编码。Python里decode()和encode()为我们提供了解码和编码的方法。其中decode('unicode_escape')能将此种字符串解码为unicode字符串。