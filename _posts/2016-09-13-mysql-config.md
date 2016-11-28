---
title: MySQL安装与配置（MacOS）
author: Li Xiang
layout: post
date: 2016-09-13 20:59:16
tags: [MySQL,Database,Configuration]
categories: [Original]
---

# 下载 MySQL

从[官方网站](http://www.mysql.com/downloads/)下载 `MySQL Community Server`。

# 安装 MySQL

在网上教程发现提到这三个文件

1. mysql-*.pkg：MySql的主要程序包
2. MySQL_StartupItem.pkg：MySql的启动项
3. MySQL.prefPane：MySQL的偏好设置，主要用来启动MySQL服务

但是打开 dmg 文件，仅仅发现一个 mysql-<version>.pkg 文件

# 安装 MySQL Workbench（GUI Tool）

仍然从官网下载。下载后安装然后进行配置。

数据库访问密码的设置

> MySQL的默认账号密码是root/root，正常情况下我们如果单纯的只是使用MySQL Workbench来管理数据库的这个账号是可以的，但是当我们在编程代码中通过jdbc来访问MySQL时我们就会发现使用这个账号是不行，无法访问，因为MySQL需要我们更改密码，也就是说root这个是个默认的密码也就是弱密码，需要我们修改之后才能在代码中使用。

# 添加到 **PATH**

将 `/usr/local/mysql/bin` 添加到 `PATH` 中
编辑 `.bash_profile` 加入 `export PATH=$PATH:/usr/local/mysql/bin`

或者

``` shell
echo "export PATH=$PATH:/usr/local/mysql/bin" >> ~/.bash_profile
```

# 报错

查询 MySQL 版本是 `mysql -v` 报错：
`Can't connect to local MySQL server through socket '/tmp/mysql.sock'`

网上寻找教程，发现有解决办法是对 `mysql.sock` 建立符号链接。但是在 Mac 上并未找到这个文件。

~~寻找 `mysql.sock` 文件：`find / -name "mysql.sock"` 得到 `/var/lib/mysql/mysql.sock`
那么建立 `symbolic link`：`ln -s /var/lib/mysql/mysql.sock /tmp/mysql.sock`~~

后来发现，这个报错是因为 `MySQL Server` 没有运行。于是打开 `MySQL.prefPane`，打开 `MySQL Server`。

又出现另外的报错 `ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)`。

检索相关问题发现导致这个报错的原因有以下三种：

1. 客户端远程访问的用户帐号并未创建；
2. 用户帐号存在，但未对其所在的客户端的 IP 进行远程访问授权允许；
3. 用户帐号授权访问的密码不正确。

看到前面安装 GUI 工具的部分说到，必须重新设置账户密码，root 的密码为弱密码。

MySQL 还有个配置文件 `my.cnf`，里面可以设置帐号密码。

**最后发现**，原来在安装 MySQL 时，弹出来一个临时密码的提醒，这个密码用于第一次登录 MySQL，并修改密码。现在终于想起来那个临时密码，但是已经忘了有没有保存。因为自己挖的坑，折腾了很久。

于是为了图方便，先把 MySQL 完全卸载。

``` shell
# first stop the database server
sudo rm /usr/local/mysql
sudo rm -rf /usr/local/mysql*
sudo rm -rf /Library/StartupItems/MySQLCOM
sudo rm -rf /Library/PreferencePanes/My*
# edit /etc/hostconfig and remove the line MYSQLCOM=-YES-
rm -rf ~/Library/PreferencePanes/My*
sudo rm -rf /Library/Receipts/mysql*
sudo rm -rf /Library/Receipts/MySQL*
sudo rm -rf /private/var/db/receipts/*mysql*
sudo rm -rf /var/db/receipts/com.mysql.*
```

然后再重新安装 MySQL。

这次长记性保存了临时密码。

接下来重新配置 MySQL。

修改根用户密码：`mysqldmin -u root -p password`
提示输入旧密码，然后输入新密码，最后确认新密码。然后会得到以下提示：
> Warning: Since password will be sent to server in plain text, use ssl connection to ensure password safety.

通过新修改的密码登录 MySQL：`mysql -u root -p`，提示输入密码，终于成功登录。

吸取教训，**一定不要完全按照网上的教程来安装配置应用程序，尽量根据官网文档**。

---

参考资料：

- [MAC下安装与配置MySQL](http://www.cnblogs.com/macro-cheng/archive/2011/10/25/mysql-001.html)
- [Can't connect to local MySQL server through socket '/tmp/mysql.sock'](http://blog.csdn.net/zzq900503/article/details/14163341)
- [Mac上MySQL报错](https://segmentfault.com/q/1010000000094608)
- [Install MySQL on Mac OS X](http://obscuredclarity.blogspot.in/2009/08/install-mysql-on-mac-os-x.html)
- [连接MySQL数据库时常见故障问题的分析与解决](http://blog.csdn.net/lioncode/article/details/7917310)
- [How do you uninstall MySQL from Mac OS X?](http://stackoverflow.com/questions/1436425/how-do-you-uninstall-mysql-from-mac-os-x)
- [Installing MySQL on OS X Using Native Packages](https://dev.mysql.com/doc/refman/5.7/en/osx-installation-pkg.html)
- [Uninstall MySql on a Mac OS X](http://community.jaspersoft.com/wiki/uninstall-mysql-mac-os-x)
- [Setting, Changing And Resetting MySQL Root Passwords](https://www.howtoforge.com/setting-changing-resetting-mysql-root-passwords)
- [Mysql password expired. Can't connect](http://stackoverflow.com/questions/33387879/mysql-password-expired-cant-connect)
