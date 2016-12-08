---
title: 报错问题解决记录
author: Li Xiang
date: 2016-12-01
layout: post
tags: [Error]
categories: [Wiki]
description: "记录遇到的所有报错的解决方法。"
---

# R

## MacOS 下 XML包依赖 libxml2 冲突

```
...
checking for xml2-config... /Users/lix/anaconda2/bin/xml2-config
USE_XML2 = yes
SED_EXTENDED_ARG: -E
Minor 9, Patch 2 for 2.9.2
Located parser file -I/Users/lix/anaconda2/include/libxml2/parser.h
Checking for 1.8:  -I/Users/lix/anaconda2/include/libxml2
...
You are trying to use a version 2.* edition of libxml
but an incompatible library. The header files and library seem to be
mismatched. If you have specified LIBXML_INCDIR, make certain to also
specify an appropriate LIBXML_LIBDIR if the libxml2 library is not in the default
directories.
ERROR: configuration failed for package ‘XML’
```

在安装 REmap 包时，安装依赖 XML 包，出现依赖错误。XML 包是解析和生成 XML 文件的 R 语言包，系统依赖 libxml2 (>= 2.6.3)。本身通过 homebrew 安装过 libxml2，发现 anaconda 也安装了 libxml2，出现冲突。

``` shell
> brew list libxml2
/usr/local/Cellar/libxml2/2.9.4/bin/xml2-config
/usr/local/Cellar/libxml2/2.9.4/bin/xmlcatalog
/usr/local/Cellar/libxml2/2.9.4/bin/xmllint
/usr/local/Cellar/libxml2/2.9.4/include/libxml2/ (47 files)
/usr/local/Cellar/libxml2/2.9.4/lib/libxml2.2.dylib
/usr/local/Cellar/libxml2/2.9.4/lib/cmake/libxml2/libxml2-config.cmake
/usr/local/Cellar/libxml2/2.9.4/lib/pkgconfig/libxml-2.0.pc
/usr/local/Cellar/libxml2/2.9.4/lib/ (3 other files)
/usr/local/Cellar/libxml2/2.9.4/share/aclocal/libxml.m4
/usr/local/Cellar/libxml2/2.9.4/share/doc/ (153 files)
/usr/local/Cellar/libxml2/2.9.4/share/gtk-doc/ (55 files)
/usr/local/Cellar/libxml2/2.9.4/share/man/ (4 files)
```

检查 homebrew 安装的 libxml2，发现版本满足 XML 包要求。报错信息提示可以定义环境变量到非默认的路径。

> If you have specified LIBXML_INCDIR, make certain to also specify an appropriate LIBXML_LIBDIR if the libxml2 library is not in the defaultdirectories.

设置环境变量：
- `export LIBXML_INCDIR=/usr/local/Cellar/libxml2/2.9.4`
- `export LIBXML_LIBDIR=/usr/local/Cellar/libxml2/2.9.4/lib`

继续安装仍然报错：提示无法找到 parser.h 文件。

```
You specified LIBXML_INCDIR, but we couldn't find parser.h
Please specify it correctly and re-run the INSTALL'ation.
ERROR: configuration failed for package ‘XML’
```

**Anaconda 与 Homebrew 冲突问题**

运行 `brew doctor` 发现一个警告：

```
Warning: Anaconda is known to frequently break Homebrew builds, including Vim and
MacVim, due to bundling many duplicates of system and Homebrew-available
tools.

If you encounter a build failure please temporarily remove Anaconda
from your $PATH and attempt the build again prior to reporting the
failure to us. Thanks!

Warning: "config" scripts exist outside your system or Homebrew directories.
`./configure` scripts often look for *-config scripts to determine if
software packages are installed, and what additional flags to use when
compiling and linking.

Having additional scripts in your path can confuse software installed via
Homebrew if the config script overrides a system or Homebrew provided
script of the same name. We found the following "config" scripts:
  /Users/lix/anaconda2/bin/curl-config
  /Users/lix/anaconda2/bin/freetype-config
  /Users/lix/anaconda2/bin/libdynd-config
  /Users/lix/anaconda2/bin/libpng-config
  /Users/lix/anaconda2/bin/libpng16-config
  /Users/lix/anaconda2/bin/python-config
  /Users/lix/anaconda2/bin/python2-config
  /Users/lix/anaconda2/bin/python2.7-config
  /Users/lix/anaconda2/bin/xml2-config
  /Users/lix/anaconda2/bin/xslt-config
```

可以看到 xml2-config 与 homebrew 下的 xml2-config 出现了冲突。

**解决：不添加 anaconda 至 PATH 中，然后重新安装 libxml2，最后成功安装 XML 包。**

# Homebrew

## Terminating active homebrew process

```
# try
/usr/bin/pkill ruby
# try
/usr/bin/pgrep ruby
# do
chown -R $(whoami) /usr/local/var/homebrew
# do
sudo rm -rf /usr/local/var/homebrew/locks
```

来源：[Terminating active homebrew process #5159](https://github.com/Homebrew/homebrew-core/issues/5159)
