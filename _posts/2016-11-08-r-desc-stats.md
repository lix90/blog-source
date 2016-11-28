---
title: R：描述性统计
author: Li Xiang
date: 2016-11-08
layout: post
tags: [R,Statistics,R-basics]
categories: [Notes]
---

获取数据表的属性：

- `str(data)` 数据构成
- 列数：`ncol(data)`
- 行数：`nrow(data)`
- 名称：`names(data)` 或者 `col.names(data)` `row.names(data)`
- 长度：`length(data)` 或者查看某一列的唯一值个数 `length(unique(data[,"col_name"]))` 或者 `length(unique(data$col_name))`

描述性统计：

直接使用 `summary(data)` 就可以得到描述性统计值。`summary` 会根据输入对象的类型而返回不同的统计值。
如果对象为 `charactor` 那么得到的是字符串总长度和 `Class` 和 `Mode`。如果对象为 `factor`，得到的是每个 `factor` 的数目。如果是 `integer`，得到的是最小值、中位数、平均数、四分位数、最大值。

如果用特定的计算统计量的函数呢？

- 最小值 `min(data$col_name)`
- 最大值 `max(data$col_name)`
- 标准差 `sd(data$col_name)`
- 方差 `var(data$col_name)`
- 均值 `mean(data$col_name)`
- 四分位数 `quantile(data$col_name, c(0.25, 0.75))`
- 中位数 `median(data$col_name)`
- 中位数绝对偏差 `mad(data$col_name)`

还有偏度和峰度两个描述性统计指标，但是 R 基本包里头没有提供直接算的函数。要么自己写一个函数，要么使用第三方开发包中的函数计算。

参考[这篇博文](http://jackycode.github.io/blog/2014/03/12/rseries5/)，作者给出了公式和代码：

``` r
desc.stats <- function(x, na.omit=FALSE {
  if (na.omit)
    x <- x[!is.na(x)]
  n <- length(x)
  mean <- mean(x)
  var <- var(x)
  sd <- sd(x)
  skew <- sum((x-mean)^3/sd^3)/n #计算偏度
  kurt <- sum((x-mean)^4/sd^4)/n - 3 #计算峰度
  return(list(Mean=mean, Variance=var, skewness=skew, kurtosis=kurt))
}
```

还有有哪些包提供了描述性统计的函数呢？

- `Hmisc` 包中的 `Hmisc::describe()` 函数，可以返回变量数目、缺失值数目、均值、分位数等；
- `fBasic` 包中有 `skewness()` 和 `kurtosis()` 函数分别计算偏度和峰度；该包还有一个 `fBasic::basicStats()` 可以得到大部分描述性统计量。
- `psych` 专门用于心理统计学的包，里头也有关于描述性统计的函数，`psych::describe()` `psych::describeData()` `psych::describeBy()`

如果按照组或者变量水平来进行描述性统计呢？

- 可以使用基本包里头的向量化运算的 `apply()` 族，`by()` `aggregate()` 等。
- Hackley 大神开发的 `plyr` 和加强版 `dplyr` 也是可以组的描述性统计的。
- 还有如 `psych::describeBy()` `doBy::summaryBy()`

参考: [Quick-R: Descriptive Statistics](http://www.statmethods.net/stats/descriptives.html)
