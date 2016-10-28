---
title: 零基础如何学习一门新的编程语言？
author: Li Xiang
layout: post
date: 2016-09-17 14:48:43
tags: [学习方法]
categories: [个人日志]
---

在正式读研之前，我几乎没有编程基础。本科在一所不知名的民办二本院校的第一届人力资源班。只在省二级计算机考试中接触了丁点儿编程（好像是VFOX）。也没有考国家计算机二级证书。从刚读研开始，需要在 MATLAB 环境下工作，才正式学起了一门程序语言。所以学习一门编程语言并没有想象中的困难。

借这个地儿，分享**如何从零基础菜鸟开始入门到熟悉并且掌握一门程序语言**的一些经验，希望能够给同样零基础，或者畏惧编程的朋友（特别是从事科学研究的人）一些启发。

P.S. 内容较为简洁，后续再补充。

# 为什么科研人员要至少学一门编程语言？

- 提高生产效率（productivity）
- 培养抽象逻辑思维（abstract thinking）
- 提高研究的可重复性，拥抱开放科学（[open science](https://en.wikipedia.org/wiki/Open_science)）
- 促进同行交流（communication）
- ......

# 对于科研工作者有哪些编程语言和工具值得一学？

- `R` `Python` `Matlab`
- `Linux` `Shell` `Git`

为什么要学习这些东西，搜索引擎检索：`why learn x as y` 或者 `Y 为什么学 X`，X 为对应的语言和工具，Y 为职业或者领域。

---

# 准备工作

## 1. 科学上网

[GFW](https://zh.wikipedia.org/zh/防火长城) 阻断了国人许多获取信息和知识的渠道。所以，要想借助互联网进行学习，首要解决的问题就是突破 GFW 的限制。

- Chrome/Firefox: 请用帐号登录浏览器，已便于同步书签；若希望跨浏览器同步书签，请使用搜索引擎检索“跨浏览器同步书签”
- [shadowsocks](https://shadowsocks.com/client.html)，请从网上获取免费或者付费帐号，不会使用请检索“如何使用shadowsocks科学上网”

## 2. 环境配置

要想舒服的学习程序语言，那么就要配置舒服的语言环境。就好像，学外语一样，得有一个很好的语言环境，学习起来才自然。初学者一定不要忽视编程环境的重要性，一定要让自己舒舒服服地写代码，编程的过程才不是枯燥乏味的，惹人烦的。所以，一定要扎扎实实把环境给配置好了，再开始系统地学。如果在进行配置上有困难，那就请教其他懂行的人，或者再多花一些时间。如果仅仅是在面对环境的配置就进行不下去了，那的确可以不用学编程了。

配置语言环境从以下三个方面进行。

- 操作系统
  + Ubuntu
  + MacOS
  + Windows 下虚拟机运行 Ubuntu
  + （Windows 下进行配置本人没有尝试过）
- 编辑器
  + 较容易：[Sublime Text](https://www.sublimetext.com/)，[Atom](https://atom.io/)
  + 较难：[Emacs](https://www.gnu.org/software/emacs/)，[Vim](http://www.vim.org/)
- 集成开发环境 IDE (Integrated development environment)
  + R: [Rstudio](https://www.rstudio.com/), Emacs (ESS)
  + Python: [IPython](https://ipython.org/), [Spyder](https://github.com/spyder-ide/spyder), [Anaconda](https://www.continuum.io/downloads), Emacs (Elpy)
  + Matlab: Matlab GUI, Emacs (matlab-mode)

---

# 学习资料

## 1. 官方文档 Documentations

- [R](https://www.r-project.org/), [Rstudio](https://support.rstudio.com/hc/en-us/categories/200035113-Documentation), [Rdocumentation](http://www.rdocumentation.org/), [Rseek](http://rseek.org/),
- [Python2.x](http://docs.python.org/2/), [Python3.x](http://docs.python.org/3/)
- [Matlab Documentation](http://cn.mathworks.com/help/)

## 2. 搜索引擎 Search Engines

- **Google Search**：[谷歌学术检索技巧](https://www.zhihu.com/question/20161362)
- DuckDuckGo
- Bing
- Baidu

## 3. 社区 Community

- 综合：[Github](https://github.com/), [StackOverflow](http://stackoverflow.com/)
- R: [统计之都](http://cos.name/), [R-bloggers](https://www.r-bloggers.com/), [Awesome-R](https://github.com/qinwf/awesome-R)
- Python: [Python China](http://python-china.org/), [Awesome-Python](https://github.com/vinta/awesome-python)
- MATLAB: [File Exchange](http://www.mathworks.com/matlabcentral/fileexchange/), [MATLAB Answers](http://cn.mathworks.com/matlabcentral/answers/index) [Awesome-MATLAB](https://github.com/mikecroucher/awesome-MATLAB)

## 4. 练习项目 Toy Projects

- 个人研究项目
- 网上公开项目（去 Google 检索或者直接去 Github 搜）

需要提及的是，R 语言有一个公益项目 [Swirl](https://github.com/swirldev/swirl) 可以在 R 的命令窗口通过交互式的方式学习 R。具体请查看 Swirl 的相关文档介绍。

## 5. 书籍 Books

准备两三本书来系统地了解一门编程语言。网上有许多免费书籍，请看 **其他线上学习资料**。

## 6. 其他线上学习资料（待更新）

前面提到的 `Awesome` 项目已经囊括了各种编程语言和其他领域的学习资源，这里仅仅提一些我看过的。

- General: [Become a Programmer, Motherfucker](http://programming-motherfucker.com/become.html)
- R: [Cookbook for R](http://www.cookbook-r.com/)，[Advanced R](http://adv-r.had.co.nz/)，[Efficient R programming](https://csgillespie.github.io/efficientR/), [Learning Statistics with R](http://health.adelaide.edu.au/psychology/ccs/teaching/lsr/),[R for Data Science](http://r4ds.had.co.nz/), [Notes on the use of R for psychology experiments and questionnaires](http://www.psych.upenn.edu/~baron/rpsych/rpsych.html)
- Python: [Think Python 第二版](http://codingpy.com/books/thinkpython2/index.html), [Python Cookbook 第三版](http://python3-cookbook.readthedocs.io/zh_CN/latest/index.html), [Statistics in Python](http://gael-varoquaux.info/stats_in_python_tutorial/)
- MATLAB：[MATLAB程式設計：入門篇](http://mirlab.org/jang/books/matlabProgramming4beginner/)，[MATLAB程式設計：進階篇](http://mirlab.org/jang/books/matlabProgramming4guru/)，[MATLAB Cookbook](http://www.matlab-cookbook.com/)

---

# 如何学习

## 第一步：从整体上了解某种语言功能、特点以及优缺点

这一步可以通过慕课或者书籍来对一门编程语言有一个大概的了解，知道它适合做什么，不适合做什么。

相关慕课请通过搜索引擎进行检索。个人不太喜欢看视频学一门编程语言，相对来说比较喜欢看书。习惯看电子书的可以访问前面提到的免费电子书。习惯看纸质书的借一本翻翻就行了。也许其他人比较喜欢看视频教学。

## 第二步：弄明白如何查询和获取帮助文档 Getting Help

以下是一些获取帮助的命令，先熟练这几个命令的用法，对后面学习其他函数和命令有非常大的帮助。并不是任何时候都需要查谷歌搜百度。通过这些命令也可以对相关编程语言进行学习。

- R: `?function` `help(function)` `help.search()` `apropos()`
- Python: `?` `??` `help()` `dir()` `__doc__`
- Matlab: `help` `doc` `lookfor`

## 第三步：熟悉基本语法和编码规范 Grammar & Style

- [Learn X in Y Minutes](https://learnxinyminutes.com/)
  + [X 分钟速成 R](https://learnxinyminutes.com/docs/zh-cn/r-cn/)
  + [X 分钟速成 Python](https://learnxinyminutes.com/docs/zh-cn/python-cn/)
  + [X 分钟速成 MATLAB](https://learnxinyminutes.com/docs/zh-cn/matlab-cn/)
- 通过 **Cheat Sheet** 来快速了解基本语法
  + [Cheatography](https://www.cheatography.com/)
  + [Cheat-Sheets.org](http://www.cheat-sheets.org/)
  + 或者谷歌检索 `cheat sheet r/python/matlab filetype:pdf` 或者 `quick reference r/python/matlab filetype:pdf`
- 代码规范 Coding Style
  + R: [Google's R Style Guide](https://google.github.io/styleguide/Rguide.xml), [R Style guide](http://adv-r.had.co.nz/Style.html)
  + Python: [PEP 8 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/), [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)
  + MATLAB: [MATLAB Style Guidelines 2.0](https://cn.mathworks.com/matlabcentral/fileexchange/46056-matlab-style-guidelines-2-0), [Matlab Coding Style](www.cs.cornell.edu/courses/cs321/2003fa/Matlab%20Coding%20Style.pdf)

## 第四步：在练习或实践中探索性地学习 Practice & Experimentation

在学习和使用编程语言的过程中，不可避免的遇到各种报错信息。这并不是不好的信号，而正式掌握一个函数或者语法时候。有时候可以故意“犯错”，看看出现什么样的报错信息。总之，多去根据文档里头的例子或者自己编个例子尝试尝试一个函数的用法。

## 第五步：阅读书籍和源码 Books & Source code

一般来说，不做程序员，就没必要学得太深入。但是如果感兴趣，要进一步提高，那就要多阅读经典技术书籍和源代码咯。

---

# Linux, Shell, & Git 学习资源

Linux
- [鸟哥的 Linux 私房菜](http://linux.vbird.org/linux_basic/)
- [Awesome Linux](https://github.com/aleksandar-todorovic/awesome-linux)

Shell
- [快乐的 Linux 命令行](http://billie66.github.io/TLCL/index.html)
- [Awesome Shell](https://github.com/alebcay/awesome-shell)

Git
- [Git Documentation](https://git-scm.com/documentation)
- [Git 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)
- [廖雪峰的 Git 教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

---

# 总结

- 在科学上网的前提下，善用**搜索引擎**；
- 学会查询和阅读**文档**；
- 在最开始就养成良好的**编程规范**；
- 探索性地**边做边学**。
