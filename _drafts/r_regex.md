---
title: 掌握 R 语言之正则表达式
author: Li Xiang
date: 2016-10-03 00:46:15
layout: post
tags: [R,正则表达式]
categories: [R]
---



> A ‘regular expression’ is a pattern that describes a set of strings.

按照文档中的定义，正则表达式是用来描述一个字符串集合的模式（pattern）。

在 R 语言中，有两类正则表达式：一是默认使用的拓展的正则表达式（extended regular expressions）；二是类 Perl 语言的正则表达式，通过 `perl = TRUE` 生效。另外还有可以通过设置参数 `fixed = TRUE` 使用 literal 正则表达式。

支持正则表达式的函数包括：
`grep` `grepl` `regexpr` `gregexpr` `sub` `gsub` `strsplit`
另外，其他函数 `apropos` `browseEnv` `help.search` `list.files` `ls` 等往往通过 `grep` 函数来支持正则表达式。

正则表达式过长可能不被接受，因为 POSIX 标准仅支持最高256字节。

# Extended Regular Expressions

- 字母和数字本身就是正则表达式，可用来匹配自身。
- 具有特殊含义的元字符需要通过反斜杠（backslash，`\`）逃逸其所代表的特殊含义。

元字符包括：`. \ | ( ) [ { ^ $ * + ?`

> Escaping non-metacharacters with a backslash is implementation-dependent. The current implementation interprets \a as BEL, \e as ESC, \f as FF, \n as LF, \r as CR and \t as TAB.

> A character class is a list of characters enclosed between [ and ] which matches any single character in that list; unless the first character of the list is the caret ^, when it matches any character not in the list.

> A range of characters may be specified by giving the first and last characters, separated by a hyphen.

> Certain named classes of characters are predefined. Their interpretation depends on the locale (see locales); the interpretation below is that of the POSIX locale.

`[:alnum:]` = `[:alpha:]` + `[:digit:]`
`[:alpha:]` = `[:lower:]` + `[:upper:]`
`[:blank:]` 空白符，如空格、tab
`[:cntrl:]` Control characters
`[:digit:]` 数字
`[:graph:]` = `[:alnum:]` + `[:punct:]`
`[:lower:]` 小写字母
`[:print:]` 可打印的字符 `[:alnum:]` `[:punct:]` 空格
`[:punct:]` 标点符号
`[:space:]` 空格符：tab, newline, vertical tab, form feed, carriage return, space, and possibly other locale-dependent characters
`[:upper:]` 大写字母
`[:xdigit:]` 十六进制数字

元字符

`.` 匹配其他任何单字符
`\w` 匹配单词 = `[[:alnum:]_]` `\W` = `[^[:alnum:]_]`
`\s` 空白符 `\S` 非空白符
`\d` 数字 `\D` 非数字
`^` 匹配首空字符（line）
`$` 匹配尾空字符（line）
`\<` 匹配首空字符（word）
`\>` 匹配尾空字符（word）
`\b` 匹配位于边缘的空字符（word）
`\B` 匹配非边缘字符（word）

匹配频率有关的元字符
`?` 匹配 1 次
`*` 匹配 0 或多次
`+` 匹配 1 或多次
`{n}` 匹配 n 次
`{n,}` 匹配 n 或更多次
`{n,m}` 匹配 n 至 m 次

默认来说，默认匹配次数是有多少次就多少次。但是可以通过 `?` 来改变低频率匹配。

正则表达式可以被连接起来，其作用等同于把待匹配的字符串用连接的正则表达式匹配的效果。两个正则表达式也可以通过 `|` 求并集。

# 正则表达式函数实例

## grep

