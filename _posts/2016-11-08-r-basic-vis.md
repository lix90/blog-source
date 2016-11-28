---
title: R：基本数据可视化
author: Li Xiang
date: 2016-11-08
layout: post
tags: [R,Data viz]
categories: [Notes]
---

最近需要分析毕业论文数据，借机温习一下常见的统计图形，并且熟悉下如何在 R 下进行数据可视化。

# 箱图 Boxplot

## 什么是箱图？ ##

箱形图，又叫箱须图（Box-Whisker Plot），是利用数据的五个特征值来描述数据的图形。这五个特征值为：最小值、第一四分位数、中位数、第三四分位数、最大值。

## 箱形图的用处 ##

- 粗略估计数据的**对称性**：由上下箱须和箱高度的长短差异表现出来
- 粗略观察数据的**离散程度**和**集中程度**：由上下箱须距离和箱的高度表现出来
- 粗略比较样本之间的特征

## 箱形图的不足 ##

- 无法精确度量数据分布的偏态和尾重程度：可通过偏态值
- 对于较大的数据集，反映的信息较为模糊
- 中位数代表总体集中程度存在局限性

## 绘制过程 ##

![箱形图](/img/boxplot.jpg)

- 计算上四分位数，中位数，下四分位数。
- 计算上四分位数和下四分位数之间的差值，即四分位数差（IQR，interquantile range）。
- 绘制箱线图的上下范围，上限为上四分位数，下限为下四分位数。在箱子内部中位数的位置绘制横线。
- 大于上四分位数1.5倍四分位数差的值，或者小于下四分位数1.5倍四分位数差的值，划为异常值（outliers）。
- 异常值之外，最靠近上边缘和下边缘的两个值处，画横线，作为箱线图的触须。
- 极端异常值，即超出四分位数差3倍距离的异常值，用实心点表示；较为温和的异常值，即处于1.5倍-3倍四分位数差之间的异常值，用空心点表示。
- 为箱线图添加名称，数轴等。

参考：

- [科学网：什么是箱线图](http://blog.sciencenet.cn/blog-255662-239993.html)
- http://web.pdx.edu/~stipakb/download/PA551/boxplot.html

## 使用 R 绘制箱图

### 基本包函数 `boxplot`

基本用法：`boxplot(x)` 或者 `boxplot(x~y, data)`

常用参数：

- `formula` `y ~ grp` `y` 为数值型向量，`grp` 为组或者因素水平。
- `range` 设定箱须的长度，默认为 1.5 个箱高，即 1.5 倍四分位数差。
- `width`
- `varwidth`
- `notch`
- `outline` 是否绘制异常值
- `names` 组标签
- `boxwex` 缩放参数
- `staplewex` 须顶端的横线的宽度（按盒宽比例）
- `outwex`
- `border` 边框颜色
- `col` 箱体的颜色
- `log` 对数坐标
- `pars` 更多绘图参数列表
- `add` 添加到当前图中
- `at` 绘制的位置

### ggplot2

`ggplot` 的绘图语法是以添加图层的形式绘制图形。虽然语法上与 `boxplot()` 存在差异，但是参数都几乎一样。

首先通过 `ggplot()` 创建图形（初始化一个 ggplot 的对象），声明输入数据和一般的图形视觉参数（aesthetic mapping，例如线形，颜色等）：

``` r
box_plot <- ggplot(data, aes(x, y, ...))
```

然后添加 `geom_boxplot` 图层（layers）：

``` r
box_plot <- box_plot + geom_boxplot(...)
```

`geom_boxplot()` 函数有以下一些参数：

- `mapping` 和 `data` 跟 `ggplot()` 的一样，当没有声明时，直接继承 `ggplot`。
- 位置：`position`
- 设置异常值的样式：`outlier.colour` `outlier.shape` `outlier.size` `outlier.stroke`
- 槽的样式：`notch` `notchwidth`
- `show.legend` 显示图例
- `coef` 等同于 `boxplot` 中的 `range`

### lattice

> The lattice package, written by Deepayan Sarkar, attempts to improve on base R graphics by providing better defaults and the ability to easily display multivariate relationships. In particular, the package supports the creation of trellis graphs - graphs that display a variable or the relationship between variables, conditioned on one or more other variables.

`lattice` 的特长在于展示多变量关系。

变量的关系通过 `formula` 表示，例如：

- `~x|A` 表示在因素 `A` 的所有水平下绘制相应的数值变量 `x` 的图形
- `y~x | A*B` `A` 和 `B` 两个因素混合条件下的 `y` 和 `x` 的关系

参考 [Quick-R: Lattice Graphs](http://www.statmethods.net/advgraphs/trellis.html)

`lattice` 中绘制箱图的函数为 `bwplot()`

## 与箱图类似的图

- Violin Plots `vioplot` 包
  - 呈现出了分布特征
- Tufte boxplot

# 散点图 Scatterplot

## 什么是散点图？

> 散点图对于绘制多变量数据非常有用。它们可帮助您确定各刻度变量之间的潜在关系。简单散点图使用二维坐标系绘制两个变量。三维散点图使用三维坐标系绘制三个变量。如果需要绘制更多的变量，则可以尝试重叠散点图和散点图矩阵 (SPLOM)。重叠散点图显示 x-y 变量的重叠对，其中每一对都以颜色或形状加以区分。SPLOM 创建一个二维散点图的矩阵，在 SPLOM 中每个变量都参照另外一个变量进行绘制。

- 保留了原始数据信息
- 展示多变量关系

## 在 R 中绘制基本的散点图

- 基本包 `plot` 顶层绘图函数：`plot(x, type="p", pch=1)`
- `ggplot2::geom_point()`

## 散点图矩阵

> 散点图矩阵是散点图的高维扩展，它从一定程度上克服了在平面上展示高维数据的困难，在展示多维数据的两两关系时有着不可替代的作用。--- [统计之都](http://cos.name/2009/03/scatterplot-matrix-visualization/)

- `graphics::pairs()` 是 R 中绘制散点图矩阵的经典函数
- `car::scatterplot.matrix()` 或者简写 `car::spm()`：可以直接指定散点图中主对角线上的绘图元素（密度图、箱线图、直方图、QQ图等）。
- `YaleToolkit::gpairs()`
- `lattice::splom()` 可以按类别绘制散点图矩阵。
- `GGally::ggpairs()` Hadley 推荐的绘制散点图矩阵的函数，用于替代 `ggplot2::plotmatrix()`

## 散点图变式或类似的图形

热图

- `gplots::heatmap.2()`
- `ggplot2::geom_raster()` `ggplot2::geom_tile()`

hexbin plot

> We can use the hexbin package in case we have multiple points in the same place (overplotting). Hexagon binning is a form of bivariate histogram useful for visualizing the structure in datasets with large n.

- `Hexbin::hexbinplot()`
- `ggplot2`: `stat_binhex()` `geom_bin2d()`

- 在散点图上添加等高线：`ggplot2::geom_density2d()`
- 对散点图进行平滑 `graphics::smoothScatter()`
- 在散点图上加上分布图或者直方图
  - 使用 `ggplot2` 分别绘制散点图和直方图，然后用 `gridExtra` 把图拼接在一起。
  - 使用 `ggplot2` 中的 `geom_rug()` 图层（rug plots）
  - 使用 `ggExtra::ggMarginal()` 添加直方图到 `ggplot` 图层上。
  - 在这里可能需要对齐图，可以用到 `gtable` 包，可以将不同的 `ggplot` 图拼接时对齐。

参考: [StackOverflow: Scatterplot with too many points](http://stackoverflow.com/questions/7714677/r-scatterplot-with-too-many-points)

# 直方图 Histogram

直方图用来展示数值型数据的分布，可以用来估计连续性数据的概率分布。直方图的纵轴为频率或者相对频率。

使用 R 绘制直方图：

`graphics::hist()`
`graphics::plot.histogram()`
`lattice::histogram()`
`MASS::hist.scott()` 可以自动指派 bin 宽度。
`MASS::truehist()`
`ggplot2::geom_histogram()`
`ggplot2::geom_freqpoly()`
`plotrix::histStack()`
`plotrix::multhist()`
`plotrix::plotH()`
`plotrix::weighted.hist()`
`psych::multi.hist()`
`psych::pairs.panels()`
`psych::scatter.hist()`

等等

# 其他统计图

Mosaic Plot 类别数据，面积大小相对比例
Heat Map 多变量关系，通过色彩深浅区分频率、密度和大小
Pareto chart 条形图+累加线图，质量控制
Sparkline 时间序列，气候，金融
Radar chart 雷达图
Line Chart 连续数据，趋势，时间序列数据
Bar Chart 类别数据，大小比较
Correlogram 相关图，展示相关矩阵

参考：[Wikipedia: List of graphical methods](https://en.wikipedia.org/wiki/List_of_graphical_methods)

# 数据可视化的几点原则

> Graphical displays should:
>
> - show the data 显示原始数据
> - induce the viewer to think about the substance rather than about methodology, graphic design, the technology of graphic production or something else 引导观察者思考内容而非其他
> - avoid distorting what the data has to say 避免扭曲真实数据要展现的东西
> - present many numbers in a small space 在较小的空间展现大量的数据
> - make large data sets coherent 让大数据集具有一致性（清晰明了）？
> - encourage the eye to compare different pieces of data 鼓励用眼睛去比较数据之间的差异
> - reveal the data at several levels of detail, from a broad overview to the fine structure 从宏观到微观揭示数据表达的信息
> - serve a reasonably clear purpose: description, exploration, tabulation or decoration 服务于合理清晰的目标：描述，探索，制表或者装饰？
> - be closely integrated with the statistical and verbal descriptions of a data set. 紧密整合统计和言语上对数据集的描述
>
> --- The Visual Display of Quantitative Information, Edward Tufte

# 统计图表所要展示的一些定量信息

参考：[Wikipedia: Data Visualization](https://en.wikipedia.org/wiki/Data_visualization)

> Quantitative messages
>
> Author Stephen Few described eight types of quantitative messages that users may attempt to understand or communicate from a set of data and the associated graphs used to help communicate the message:
>
> - **Time-series**: A single variable is captured over a period of time. A line chart may be used to demonstrate the trend. 时序，随着时间发展而变化
> - **Ranking**: Categorical subdivisions are ranked in ascending or descending order. A bar chart may be used to show the comparison across the sales persons. 顺序，类别之间的大小顺序
> - **Part-to-whole**: Categorical subdivisions are measured as a ratio to the whole. A bar chart can show the comparison of ratios. 部分相对于整体的比例
> - **Deviation**: Categorical subdivisions are compared against a reference. A bar chart can show comparison of the actual versus the reference amount. 变异，与参考对象进行比较
> - **Frequency distribution**: Shows the number of observations of a particular variable for given interval. A histogram, a type of bar chart, may be used for this analysis. A boxplot helps visualize key statistics about the distribution, such as median, quartiles, outliers, etc. 频率分布
> - **Correlation**: Comparison between observations represented by two variables (X,Y) to determine if they tend to move in the same or opposite directions. A scatter plot is typically used for this message. 相关性
> - **Nominal comparison**: Comparing categorical subdivisions in no particular order. A bar chart may be used for this comparison. 类别比较，无特定顺序
> - **Geographic or geospatial**: Comparison of a variable across a map or layout. A cartogram is a typical graphic used. 地理和空间信息
