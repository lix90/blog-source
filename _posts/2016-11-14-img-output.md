---
title: 实验室内部分享一：绘制和编辑可发表的图形
author: Li Xiang
date: 2016-11-14
layout: post
tags: [学术出版,统计图表,Illustrator,Photoshop,Inkscape,矢量图,位图,Lab]
categories: [Original]
---

本文为实验室内部分享内容提纲。
分享目的：做到在不求人的情况下无痛高效地输出符合论文投稿要求的图形。

# 准备知识

## 颜色模式

- 印刷：CMYK，印刷三原色（青品黄），叠加变暗 ---> 打印出版
- 显示：RGB，光影三原色（黄绿蓝），叠加变亮 ---> 在线出版
- 其他：HSB, Lab, 位图模式，灰度模式，索引颜色模式，双色模式，多通道模式等

## 图形格式

类型 | 定义 | 特点 | 常见格式
:---|:----|:-----|:--------
矢量图 | 使用点、线、面（多边形）等基于数学方程的几何图元表示的图像 | 放大缩小图形质量不变 | eps, svg, pdf, ...
位图 | 使用像素阵列表示的图像 | 尺寸放大会影响质量 | jpg, png, tiff, ...

## 图形分辨率

分辨率：两侧或者显示系统对细节的分辨能力。
PPI/DPI 单位：表示打印图像或显示器单位面积上像素/点数量的指数。

PPI
- 每英寸像素数
- 用于电脑显示领域
- 人类肉眼能够分辨的最高像素点密度为 300ppi

DPI
- 每英寸点数
- 用于打印或印刷领域


# 图形编辑软件使用

- Adobe Illustrator 商业矢量图编辑软件：**主要内容**
- Adobe Photoshop 商业位图编辑软件
- Inkscape 免费开源矢量图编辑软件

## 基本界面

- 菜单栏
- 工具栏
- 控制面板
- 图形窗口

## 快捷键

- 工具选择快捷键：快速切换当前工具
- 组合快捷键：快速操作对象，选择功能等

## 常用工具与概念

### 对象

- 对象：具有一定属性的点，线，面（填充）等
- 对象的基本操作：移动，旋转，镜像，拷贝 ...
- 建立组与取消组：建立组方便对整体进行操作。

### 选择

- 一般选择与直接选择（组选择）
- 相似对象选择：选择文本对象，选择单独的点，...
- 相似属性选择：选择具有相同描边的对象，选择具有相同填充的对象，...

### 图层

- 操作图层：删除，新建，隐藏，锁定
- 管理图层：移动，合并，重命名

### 其他重要操作

- 路径查找：Window >>> Pathfinder
- 排列对齐：Window >>> Align
- 字体描边：Type >>> Create Outline
- 取色：工具栏 >>> Eye droper tool
- 属性修改（线）：Window >>> Appearance

# 实例

1. 实验流程图
2. 单图编辑
3. 多图合并
4. ERP 线图编辑
5. ...

# 绘制图表

- 编程语言：R, Python, Matlab, ... >>> 推荐学习
- 界面操作：Excel, SPSS, JASP, ...
- 在线绘制：plot.ly, ...