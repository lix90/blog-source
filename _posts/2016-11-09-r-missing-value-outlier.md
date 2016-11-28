---
title: R：处理缺失值
author: Li Xiang
date: 2016-11-09
layout: post
tags: [R,Statistics,数据分析,缺失值]
categories: [Notes]
---

由于最近在分析毕业论文数据，顺便复习和学习新的数据分析方法，本文纯属搬运和整理他人的分享。

# 缺失值处理

`mice` 包是专门用来处理缺失值的 R 语言包。可以通过 `mice::md.pattern()` 查看缺失值的“数据模式”。

## 删除记录/样本

在 R 中，通过 `na.action = na.omit` 删除包含有缺失值的观测行。但需要满足两个条件：
- 有足够的样本点；
- 不会引入偏差。

## 删除变量/属性

如果数据集中某个特定变量包含较多的缺失值，并且删除这个变量能够保留更多的观测值。如果该变量不太重要，那么可以删除它。该方法需要权衡变量的重要性和观测值数量。

## 使用均值/中位数/众数进行插补

这是一种比较简单粗暴的方法，如果该变量对因变量的影响较小，该方法是可以接受的。但是，很可能人为增加噪音。

## 预测法

可使用的方法包括：KNN差值，rpart包，mice包。

### kNN 差值法

`DMwR::knnImputation()` 函数使用 k 近邻方法来填充缺失值。

> 具体过程如下：对于需要插值的记录，基于欧氏距离计算k个和它最近的观测。接着将这k个近邻的数据利用距离逆加权算出填充值，最后用该值替代缺失值。

### rpart

kNN 插值法的缺点对因子类变量的插补效果不好。rpart 的优点是只需一个未缺失值就可以填充整个数据样本。

### mice

> mice 是链式方程多元插值的简写（Multivariate Imputation by Chained Equations）。mice包提供了多种先进的缺失值处理方法。它使用一种不同寻常的方法来进行两步插值：首先利用mice函数建模再用complete函数生成完整数据。mice(df)会返回df的多个完整副本，每个副本都对缺失的数据插补了不同的值。complete()函数则会返回这些数据集中的一个（默认）或多个。

参考资料：
- [雪晴数据网：R语言处理缺失值的若干方法](http://www.xueqing.tv/cms/article/185)[原文](http://datascienceplus.com/missing-value-treatment/)
- [datascience+: Imputing Missing Data with R; MICE package](http://datascienceplus.com/imputing-missing-data-with-r-mice-package/)
- [如何处理数据中的缺失值](http://www.zhaokv.com/2016/01/missing-values.html)
