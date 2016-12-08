---
title: R：使用基本包进行多图布局
author: Li Xiang
date: 2016-11-16
layout: post
tags: [R,Data viz]
categories: [Original]
---

# Layout 布局

`layout` 函数可以指定复杂的绘图布局。该函数可以将设备的面板根据第一个参数 `mat` 矩阵分割为多个行和列，列宽和行高在对应的参数中指定。

``` r
layout(mat, widths = rep.int(1, ncol(mat)),
    heights = rep.int(1, nrow(mat)),
    respect = FALSE)
```
`layout.show(n)` 显示当前布局。`n` 为显示的图形的个数。`n=1` 则显示第一个图形的布局，`n=2` 则显示前两个图形的布局。
`layout` 返回的值为图形的个数。

参数：
- `mat`：矩阵对象，指定接下来的 N 个图形的位置。矩阵中的值必须为 0 或者正整数。
- `widths`：向量对象，指定列宽。可以通过数值指定相对宽度。而绝对宽度通过 `lcm()` 指定。
- `heights`：向量对象，指定列高。高度设置跟 `widths` 一样。
- `respect`：要么逻辑值要么矩阵对象。如果为矩阵对象，那么必须与 `mat` 具有同样的维度，而且每个值为 0 或者 1。该参数控制列宽的单位是否与行高的单位在设备物理测量上相同，控制设备的纵横比。纵横比为列数比上行数。如果 `respect = TRUE` 那么列宽和行高单位相同，不受页面纵横比的影响。如果 `respect = FALSE`，那么一行的高和一列的宽不一样，会受到页面的影响。
- `n`：绘制的图形个数。

需要注意的是，`layout` 布局与 `par(mfrow)` `par(mfcol)` `split.screen` 完全不兼容。

# Par 的 mfrow 和 mfcol 参数布局

`par` 用于设置或查询绘图参数。`par` 的合法参数都能在高阶绘图函数中使用。
在 `par` 的众多参数中，有两个参数可以用于多图的布局，即 `mfrow` 和 `mfcol`。

## par 关于布局的参数

**Outer margin** 外边缘

默认没有外边缘。可以通过 `oma` 增加外边缘，其单位为线宽，即一行文字的空间。还有 `omi` 和 `omd` 设置外边缘宽度，单位分别为英寸和 NDC 归一化坐标。
- `oma` 向量 `c(bottom, left, top, right)`，外边缘尺寸，行高
- `omd` 向量 `c(x1,x2,y1,y2)` 外边缘定位，单位为 NDC，即`c(left,right,bottom,top)`
- `omi` 向量 `c(bottm, left, top, right)` 外边缘尺寸，英寸

**Inner region** 内区域

为除去外边缘之外剩余的区域。如果只有一个图，那么就等于 figure region。如果有多个图，那就是多个图合并的区域。

**Figure region** 图形区域

受到外边缘和图的个数的影响。绘图区域通过 `fig` 和 `fin` 参数设定。`fig` 用来定位，`c(left, right, bottom, top)`，其中的值为内区域的大小（除去外边缘之后的区域）。`fin` 用于设定绘图区域大小，`c(width,height)`，单位为英寸，最后绘图区域将在内区域中居中。

**Figure margin** 图形边缘

图形边缘，通过 `mar` 和 `mai` 参数设定。
- `mai` 数值向量 `c(bottom, left, top, right)` 绘图边缘的尺寸，英寸
- `mar` 数值向量 `c(bottom, left, top, right)` 指定绘图边缘尺寸，行高，默认为 `c(5,4,4,2)+0.1`
- `mex` 行尺寸扩展因子，用于描述绘图边缘上的坐标。并不改变字体大小，而是指定用来转换 `mar` 和 `mai` 以及 `oma` 和 `omi` 的文本行尺寸。
- `mgp` 边缘行（`mex` 单位），用于轴标题、标签和线。`mgp[1]` 影响 `title`,`mgp[2:3]` 影响坐标轴。默认为 `c(3,1,0)`。

**Plot region** 绘制区域

- `plt` 向量 `c(x1,x2,y1,y2)` 图形区域的坐标 (left, right, bottom, top)
- `ply` 字符，指定图形区域类型，`"s"` 为正方形绘图区域，`"m"` 为最大绘图区域。
- `pin` 尺寸，`c(width, height)`

子图或多图绘制

- `mfcol, mfrow` 向量 `c(nr, nc)`，绘制 nr*nc 子图矩阵。
- `mfg` 向量 `c(i,j)` 表示接下来图形绘制的位置。必须实现定义好 `mfcol` 或者 `mfow`。另外，为了兼容 `S` 语言，还可以以 `c(i,j,nr,nc)` 的形式指定位置。

# Split.screen 布局

`split.screen` 定义在当前设备上一定数量的区域，可以在一定程度上当作独立/分离的图形设备。
`screen` 用于选择哪一个 screen 绘制图形。
`erase.screen` 用于清除一个 screen，通过填充背景颜色。
`close.screen` 移除指定的 screen。

`split.screen` 参数：
- `figs` 两个元素的向量，描述了在一个屏幕矩阵中的行和列的数目，或者一个4列矩阵。如果是矩阵，那么每一行描述了一个屏幕的左、右、下和上端的值，为 NDC 单位，即0为最左下角，1为最右上角。
- `screen` 用于分割的屏幕编号。默认为当前屏幕，否则为整个设备区域。
- `erase` 逻辑值，是否清空选中的屏幕。
- `n` 代表将准备用于绘制、擦除、或者关闭的屏幕编号。
- `new` 逻辑值，代表着是否擦除当前屏幕用于新图的绘制。
- `all.screens` 逻辑值，是否关闭所有屏幕。

``` r
split.screen(c(2,2)) # 构建两行两列的 screen
screen(2) # 选中第2个 screen
split.screen(c(2,1)) # 将第2个 screen 再次分割为两行
screen(4) # 选中第4个 screen
plot(10:1)
erase.screen() # 擦除当前 screen
plot(15:1) # 继续在当前 screen 上绘制
```

NDC：normalized device coordinates
