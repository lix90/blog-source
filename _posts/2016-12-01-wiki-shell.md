---
title: shell 命令整理
author: Li Xiang
date: 2016-12-01
layout: post
tags: [Shell]
categories: [Wiki]
description: "使用 shell 过程中的笔记。"
---

@2016-11-16

`ps` 返回正在运行的进程的信息
`ps aux` 列出所有运行进程
`ps aux | grep string` 列出匹配字符串的进程

使用 `$HOME` 替代 `~`
使用 `type -p` 替代 `which`

@2016-12-01

修改 MacOS 计算机名
`scutil --set ComputerName <computer_name>`

格式化磁盘为 Mac OS Extended Journaled (JHFS+)
`diskutil erasedisk JHFS+ <disk_name> <disk_directory>`
其他格式:
- FAT32: MS-DOS fat32
- HFS+: Mac OS Extended (HFS+)
- ExFAT

lsof 列出已打开的文件以及对应的进程
