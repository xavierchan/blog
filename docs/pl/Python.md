---
title: Python 
date: 2018-05-24 23:12:20
tags:
- python
categories:
- 编程语言
---
pip freeze > {filename}

CPython：是用C语言实现Pyhon，是目前应用最广泛的解释器。最新的语言特性都是在这个上面先实现，基本包含了所有第三方库支持，但是CPython有几个缺陷，一是全局锁使Python在多线程效能上表现不佳，二是CPython无法支持JIT（即时编译），导致其执行速度不及Java和Javascipt等语言。于是出现了Pypy。

Pypy：是用Python自身实现的解释器。针对CPython的缺点进行了各方面的改良，性能得到很大的提升。最重要的一点就是Pypy集成了JIT。但是，Pypy无法支持官方的C/Python API，导致无法使用例如Numpy，Scipy等重要的第三方库。这也是现在Pypy没有被广泛使用的原因吧。

而PyPy与CPython的不同在于，别的一些python实现如CPython是使用解释执行的方式，这样的实现方式在性能上是很凄惨的。而PyPy使用了JIT(即时编译)技术，在性能上得到了提升。

Python的解释器：

1、由于Python是动态编译的语言，和C/C++、Java或者Kotlin等静态语言不同，它是在运行时一句一句代码地边编译边执行的，而Java是提前将高级语言编译成了JVM字节码，运行时直接通过JVM和机器打交道，所以进行密集计算时运行速度远高于动态编译语言。 

2、PyPy，它使用了JIT（即时编译）技术，混合了动态编译和静态编译的特性，仍然是一句一句编译源代码，但是会将翻译过的代码缓存起来以降低性能损耗。相对于静态编译代码，即时编译的代码可以处理延迟绑定并增强安全性。绝大部分 Python代码都可以在PyPy下运行，但是PyPy和CPython有一些是不同的。
