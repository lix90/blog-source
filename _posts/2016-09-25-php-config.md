---
title: PHP 安装与配置
author: Li Xiang
layout: post
date: 2016-09-25 21:00:45
tags: [PHP,配置]
categories: [PHP]
---

为了了解 PHP 这门所谓的“世界上最好的语言”，特意安装和配置了 PHP 环境。

因为系统是 Mac OSX，所以直接使用 `brew install php56` 来安装。但是并未找到 php56 。于是 `brew search php`，发现 php 相关安装包位于 `/homebrew/php/*`，于是用 `brew install homebrew/php/php56` 安装。但是出现报错 `undefined method rebuild` 的错误。尝试 `brew cleanup && brew update`，仍然不起作用，依旧报错。后来查询到可以更新下 homebrew 的仓库。于是

``` shell
cd $(brew --repo)
git fetch
git reset --hard origin/master
brew update
```

然后再尝试安装 `brew install homebrew/php/php56`。

其实也可以这样：

``` shell
brew tap homebrew/dupes
brew tap homebrew/versions
brew tap homebrew/homebrew-php
brew install php56
```

然后安装了包管理工具 composer
> PHP 世界的包管理工具Composer

``` shell
brew install homebrew/php/composer
```

并且安装了 psySH
> A runtime developer console, interactive debugger and REPL for PHP.

``` shell
composer g require psy/psysh:@stable
```
psySH 的二进制文件位于 `~/.composer/vendor/psysh`
也可以通过这个来运行 `~/.composer/vendor/bin/psysh`
为了方便，我将其添加到 PATH `export $PATH:/Users/lix/.composer/vendor/bin`

配置 emacs 的 php 环境
先安装 ac-php 的依赖 `brew install cscope`

``` emacs-lisp
;;; php mode
(use-package php-mode
  :ensure t
  :mode "\\.php\\'"
  :config
  (progn
    (add-hook 'php-mode-hook 'smartparens-mode)
    (use-package ac-php
      :ensure t
      :config
      (add-hook 'php-mode-hook
                '(lambda ()
                   (use-package company-php :ensure t)
                   (company-mode t)
                   (add-to-list 'company-backends 'company-ac-php-backend))))
    (use-package php-eldoc
      :ensure t
      :config
      (add-hook 'php-mode-hook 'php-eldoc-enable))))

;;; php REPL
(use-package psysh
  :if (executable-find "psysh")
  :ensure t
  :defer t
  :config
  (add-hook 'psysh-mode-hook 'smartparens-mode))
```
