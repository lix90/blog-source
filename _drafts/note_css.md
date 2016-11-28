---
title: CSS 入门学习记录
author: Li Xiang
date: 2016-10-18 23:11:24
layout: post
tags: [CSS,前端开发]
categories: [CSS]
---

# 三种添加样式的方法

## 内联样式 ##

在 HTML 内通过对单个元素增加 `style` 属性。`style` 属性的值为没有花括号的声明区块。例如 `style="property: value;"`。这种引入方式有较大的局限。不能使用伪类，也不能使用 `@import` 方法。

## 嵌入式样式 ##

在 HTML 头部 `head` 元素通过 `style` 元素嵌入样式表。例如：

``` css
<style>
selector {
    property: value;
}
</style>
```

## 外部样式表 ##

外部样式表有几个好处：

- 方便更新样式表；
- 缓存外部样式表，可以降低带宽的使用；
- 可重复使用；

### `@import` 指令 ###

一个或多个 `@import` 指令可以在样式表开始部分引入外部样式表。例如：`@import url(external.css);`。

### `link` 元素 ###

link 可用于将外部样式表引入 HTML 中。这种方法允许多个 link 元素的使用。`media` 属性可用于限制一个样式表用于一种或多种媒体（媒介）。

``` html
<link href="external.css" rel="stylesheet" media="all"/>
<link href="external.css" rel="stylesheet" media="screen"/>
<link href="external.css" rel="stylesheet" media="print"/>
```
这种方法还可以引入备用样式表（alternative stylesheet）。

# 样式表优先级 #

计算选择器权重

继承关系

The Cascade

---

2016-10-20 23:36:11

# 元素显示 #

两种模式：块级和行内

## 块级 ##

块级元素的宽度填满整个父元素的内容区域，边上不允许有其他元素。块级元素在元素两端相当于断行了。常见的块级元素包括 `p` 和 `div`。

---

# 定位 Position #

static 是默认值。任意 `position: static;` 的元素不会被特殊的定位。一个 static 元素表示它不会被定位，一个 position 属性设置为其他值表示它会被定位。

在没有添加额外的属性之前，relative 表现和 static 一样。在一个相对定位的元素上设置 top、right、bottom、left 属性会使其偏离其正常位置。其他的元素则不会调整位置来弥补它偏离后剩下的空隙。

一个固定定位（position 属性的值为 fixed）元素会相对于视窗来定位，这意味着即便页面滚动，它还是会停留在相同的位置。和 relative 一样，top 、 right 、 bottom 和 left 属性都可用。

absolute 与 fixed 的表现类似，除了它不是相对于视窗而是相对于最近的已被定位的祖先元素。如果绝对定位（position属性的值为absolute）的元素没有已被定位的祖先元素，那么它是相对于文档的 body 元素，并且它会随着页面滚动而移动。

# 浮动 Float #

Float 可用于实现文字环绕图片。

# 文档流 #

文档流，即常规流（normal flow）：元素按照其在 HTML 中的位置顺序决定排布的过程，主要的形式是自上而下，一行接一行，每一行从左至右。

定位方案（Positioning schemes）分三种：

- 常规流：俗称的文档流，包含三种类型：块级元素的块级格式，行内元素的行内格式，以及两种元素的相对定位方式。
- 浮动（float）
- 绝对定位（absolute positioning）：包含 `absolute` 和 `fixed` 两种。

---

参考资料：

- [CSS 定位与文档流](http://www.ituring.com.cn/article/198258)
