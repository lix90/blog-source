---
title: R：数据导入
author: Li Xiang
date: 2016-11-08
layout: post
tags: [R,R-basics]
categories: [Original]
---

# 导入 CSV 数据

使用基本包函数

`read.csv()`

使用 `readr` 包

``` r
## wrapper function of data loading for reusing
importdata <- function(d,f) {
  data <- readr::read_csv(
                   file = file.path(d, f),
                   col_names = TRUE,
                   na = "NULL",
                   trim_ws = TRUE)
}
## load data
data <- importdata(input_dir, input_file)
```

# 导入 EXCEL 数据

# 导入 SPSS 数据
