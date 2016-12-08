---
title: 环境和工具配置
author: Li Xiang
date: 2016-12-01
layout: post
tags: [Configuration]
categories: [Wiki]
description: "记录各种开发环境和工具的配置过程。"
---

# Python

放弃使用 Anaconda 发行版，改为直接手动配置环境。

## PyPi

### MacOS 配置 pip

1. 安装 easy_install
`curl https://bootstrap.pypa.io/ez_setup.py -o - | sudo python`
2. 安装 pip
`sudo easy_install pip`
或通过 Homebrew 安装 python，会一同安装 pip
或直接使用 Anaconda 等发行版，自带 pip

### 镜像源

pipy国内镜像目前有：

http://pypi.douban.com/simple  豆瓣
http://pypi.hustunique.com/simple  华中理工大学
http://pypi.sdutlinux.org/simple  山东理工大学
http://pypi.mirrors.ustc.edu.cn/simple  中国科学技术大学
http://mirrors.aliyun.com/pypi/simple 阿里云
清华大学
公网：http://e.pypi.python.org/simple
教育网：http://pypi.tuna.tsinghua.edu.cn/simple

Linux 和 MacOS 系统下配置文件位置: `$HOME/.pip/pip.conf`
Windows 系统下配置文件位置: `%HOME%\pip\pip.ini`

设置环境变量 `PIP_CONFIG_FILE` 可以指定默认配置文件路径。

修改配置文件内容：
```
[global]
trusted-host = mirrors.aliyun.com
index-url = http://mirrors.aliyun.com/pypi/simple
```

### 其他配置

另外还可以添加其他参数：

```
[global]
timeout = 60

[freeze]
timeout = 10

[install]
ignore-installed = true
no-dependencies = no # or yes
```

对于 easy_install 可以修改 `$HOME/.pydistutils.cfg`

```
[easy_install]
index_url = <mirror>
```

另外还可以创建别名

```
alias pip="pip -i <mirror>"
```

### pip 常用命令

搜索模块
`pip search <pkg_name>`

安装模块
`pip install <pkg_name>`
`pip install <pkg_name>==<version>`

升级模块（如果不提供版本号，升级到最新版本）
`pip install --upgrade <pkg_name>>=<version>`

卸载模块
`pip uninstall <pkg_name>`

显示当前环境中模块的清单
`pip freeze`
重定向到文本文件
`pip freeze > req.txt`
使用清单
`pip install -r req.txt`

## 环境管理

使用虚拟环境管理工具

virtualenv [doc](https://virtualenv.pypa.io/en/stable/)
virtualenvwrapper [doc](https://virtualenvwrapper.readthedocs.io/en/latest/)

virtualenvwrapper 是对 virtualenv 的一系列扩展，包括创建和删除虚拟环境的包装工具，用于管理开发环境。

配置流程

``` shell
pip install virtualenvwrapper
export WORKON_HOME=~/pyEnvs
mkdir -p $WORKON_HOME
source /usr/local/bin/virtualenvwrapper.sh
mkvirtualenv env1
lssitepackages
mkvirtualenv env2
workon env1
echo $VIRTUAL_ENV
mkvirtualenv -p /usr/bin/python2 env27
mkvirtualenv -p /usr/bin/python3 env3
```

# Homebrew

## 镜像源

[Homebrew 镜像源](http://heepo.github.io/%E5%B7%A5%E5%85%B7/2015/08/05/Homebrew-Mirror-Links.html)
[HomeBrew中国镜像源](http://blog.haohtml.com/archives/16915)
[换源让Homebrew速度飞起！一起brew吧！](https://maomihz.com/2016/06/tutorial-6/)

最后修改镜像不成功，太麻烦，放弃折腾，改回了官方 github 源。
# MacOS 配置
## Time machine

- 准备移动硬盘，做好备份
- 移动硬盘分出一个300GB左右的分区，格式化为 Mac OS Extened Journaled 格式。
- 然后选择该分区作为备份空间，开始备份并且加密

参考
- [Mac下移动硬盘的分区以及TimeMachine的备份](http://www.jianshu.com/p/5f8b4d9a8922)
- [少数派 Time Machine 使用教程](http://sspai.com/tag/Time%20Machine)
## 卸载 Rime 输入法

这个所谓的“程序员”用的输入法，实在是没用习惯。@2016-12-02 喜欢能简则简的我，改用苹果系统自带中文输入法。

``` shell
$ killall Squirrel
$ sudo rm -Rf "/Library/Input Methods/Squirrel.app"
$ rm -Rf ~/Library/Rime
```
