---
title: 如何查看 R 语言的函数和方法的源代码
author: Li Xiang
date: 2016-10-08 22:23:57
layout: post
tags: [R]
categories: [R]
---

从网上搜集了一些如何查看 R 语言函数和方法的源代码的方法。

<!--more-->

话说人丑就要多读书，程序员写的代码丑要多读源代码。为了深入了解 R 语言各种统计方法函数的背后的逻辑和艺术，谷歌了下一些阅读源代码的方法。以 `t` 函数总结如下。

函数类型
- in-built 函数
- S3 函数
- S4 函数
- unexported functions
- compiled code
- infix operators

首先，函数不带括号直接执行，会看到

`methods`
`getAnywhere`

`UseMethod(t)` 提示你 `t()` 是一个 `S3` 范型函数，不同的对象类型对应不同的方法。

`selectMethod`
`getMethods`
`findMethods`

问题：什么是 `S3` 范型函数？
问题：什么是 `S4` 范型函数？

通过 `showMethods("function")` 得到对应的对象；
然后使用 `getMethod("function", "object")` 得到源代码。

---
参考资料：
- [How can I view the source code for a function?](http://stackoverflow.com/questions/19226816/how-can-i-view-the-source-code-for-a-function)
- [What does “S3 methods” mean in R?](http://stackoverflow.com/questions/6583265/what-does-s3-methods-mean-in-r/6583639#6583639)
- [Get source codes for invisible functions or internal functions in R](http://yusung.blogspot.jp/2007/08/get-invisible-functions-or-internal.html)
- [How do I show the source code of an S4 function in a package?](http://stackoverflow.com/questions/5937832/how-do-i-show-the-source-code-of-an-s4-function-in-a-package)
