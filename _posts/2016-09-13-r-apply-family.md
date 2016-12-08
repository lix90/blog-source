---
title: R：向量化运算
author: Li Xiang
layout: post
date: 2016-09-13 22:50:21
tags: [R,R-basics]
categories: [Notes,R]
---

> Updated in 2016-11-12

学习 `sapply` `lapply` `apply` `tapply` `by` `aggregate` 等向量化运算函数的笔记。

# `apply`

当输入数据为矩阵或数组时使用，如果输入数据为 `data.frame`，则不建议使用。

`apply(X, MARGIN, FUN, ...)`

- `X` 数组或矩阵
- `MARGIN` 指定 `FUN` 作用的由下标组成的向量。若 `X` 为矩阵，1 表示行，2 表示列。`c(1,2)` 表示行和列。如果 `X` 包含 `dimnames`，那么也可以为字符向量。
- `FUN` 使用的函数

如果需要在行或者列上求均值和求和，则建议使用 `colMeans` `rowMeans` `colSums` `rowSums`。

# `tapply`

需要对向量按组或者因素水平计算，类似于 `split-apply-combine`。

# `by`

可替代 `tapply`，在无法使用 `tapply` 的情况下仍然可用。

[参考](http://stackoverflow.com/a/32262439/6469987)

# `aggregate`

跟 `tapply` 类似，不同的是，`aggregate` 的第二个参数必须为 list，输出为 data.frame。`aggregate` 的参数还可以为 formula。需要主要的是 `aggregate` 的 formula 方法默认 `na.action = na.omit`，所以需要手动设置参数 `na.rm = TRUE`。

# `lapply`

输入和输出都为 list。其他 `*apply` 函数底层都是调用 `lapply` 函数。

`lapply(X, FUN, ...)`

返回与 `X` 等长度的 list，每个元素是由 `X` 中的元素经过 `FUN` 计算得到。

# `sapply`

输入为 list，但输出为 vector。

`sapply(X, FUN, ..., simplify = TRUE, USE.NAMES = TRUE)`

比 `lapply` 更友好，虽然默认返回 vector，matrix，但是如果增加 `simplify = "array"` 的参数，将返回 array。`sapply(x, f, simplify=FALSE, USE.NAMES = FALSE)` 等同于 `lapply(x, f)`。

# `vapply`

`vapply(X, FUN, FUN.VALUE, ..., USE.NAMES = TRUE)`

类似与 `sapply`，但是返回值的类型是事先确定。

# `replicate`

重复地执行表达式。


# 其他相关函数

`outer` `ave` `eapply`

# 比较好的总结

> - **lapply** is a list apply which acts on a list or vector and returns a list.
> - **sapply** is a simple lapply (function defaults to returning a vector or matrix when possible)
> - **vapply** is a verified apply (allows the return object type to be prespecified)
> - **rapply** is a recursive apply for nested lists, i.e. lists within lists
> - **tapply** is a tagged apply where the tags identify the subsets
> - **apply** is generic: applies a function to a matrix's rows or columns (or, more generally, to dimensions of an array)

[参考](http://stackoverflow.com/a/23282110/6469987)

---

参考资料

- [R Grouping functions: sapply vs. lapply vs. apply. vs. tapply vs. by vs. aggregate](https://stackoverflow.com/questions/3505701/r-grouping-functions-sapply-vs-lapply-vs-apply-vs-tapply-vs-by-vs-aggrega)
