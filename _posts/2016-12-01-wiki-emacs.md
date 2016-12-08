---
title: Emacs 个人参考
author: Li Xiang
date: 2016-12-01
layout: post
tags: [Emacs]
categories: [Wiki]
description: "使用 Emacs 过程中的记录。"
---

# markdown-mode #

总是容易忘记 markdown mode 的快捷键，这回刻意记下常用的快捷键。

在 markdown-mode 下，打开帮助文档 <kbd>C-h m</kbd>（我自己将 <kbd>C-h</kbd> 改为了 <kbd>f1</kbd>）。markdown-mode 的 key-map 的前缀命令为 <kbd>C-c</kbd>，也就是按这个键能调出与 markdown-mode 有关的一些命令的快捷键。

## 对标题的操作 ##

- `<M-S-down/up>` `markdown-move-subtree-down/up` 向下或向上移动标题。
- `<M-S-left/right>` `markdown-promote/demote-subtree` 标题升级或降级。
  - 当标题为 `# title #` 通过 `<M-S-left>` 得到 `title`；`<M-S-right>` 得到 `## title ##`。
  - 最低级数为第六级 `###### title ######`。
- `<M-left/right>` `markdown-promote/demote` 循环改变标题级数（升或降）。
- `<S-tab>` `markdown-shifttab` 折叠标题内容
- `C-c C-t 1/2/3/4/5/6` `markdown-insert-header-atx-1/2/3/4/5/6`

## 跳转与移动 ##

跳转标题
- `C-c C-b/f` `markdown-backward/forward-same-level` 同级跳转（后或前）。
- `C-c C-n/p` `markdown-next/previous-visible-heading` 标题跳转（后或前）。

跳转链接
- `M-n/p` `markdown-next/previous-link`
- `M-{/}` `markdown-backward/forward-paragraph`

## 添加内容 ##

|   |   |
:--|:--|:--
列表 | `<M-RET>` `C-c C-j` | `markdown-insert-list-item`
添分隔符 | `C-c -` | `markdown-insert-hr`
添加行引用 | `C-c C-s b` | `markdown-insert-blockquote`
块引用 | `C-c C-s C-b` | `markdown-blockquote-region`
行代码 | `C-c C-s c` | `markdown-insert-code`
代码块 | `C-c C-s P` | `markdown-insert-gfm-code-block`
斜体 | `C-c C-s e` | `markdown-insert-italic`
加粗 | `C-c C-s s` | `markdown-insert-bold`
键盘 | `C-c C-s k` | `markdown-insert-kbd`
行预排格式文本 | `C-c C-s p` | `markdown-insert-pre`
块预排格式文本 | `C-c C-s C-p` | `markdown-pre-region`
引用图片 | `C-c TAB I` | `markdown-insert-referent-image`
图片 | `C-c TAB i` | `markdown-insert-image`
脚注 | `C-c C-a f` | `markdown-insert-footnote`
链接 | `C-c C-a l` | `markdown-insert-link`
网址 | `C-c C-a u` | `markdown-insert-uri`
wiki链接 | `C-c C-a w` | `markdown-insert-wiki-link`

# help-mode #

用于阅读帮助文档和跳转文档内引用的主要编辑模式（Major mode）

Key | binding
:--|:--
`TAB` | forward-button 下一个按钮/链接
`S-TAB` | backward-button 上一个按钮/链接
`SPC` | scroll-up-command 向下滚动内容
`DEL`/`S-SPC` | scroll-down-command 向上滚动内容
`<` | beginning-of-buffer 缓冲区开始
`>` | end-of-buffer 缓冲区末尾
`?`/`h` | describe-mode 描述模式
`g` | revert-buffer 更新
`l`/`C-c C-b` | help-go-back 回退
`r`/`C-c C-f` | help-go-forward 前进
`q` | quit-window 推出帮助窗口
`RET`/`C-c C-c` | help-follow-symbol 跳转到光标处的符号

# ess-help-mode

## 导航 ##

key | binding
:---|:-------
`<` | 移动到 buffer 顶端
`>` | 移动到 buffer 末端
`RET` | 移动到下一行
`SPC` | 向下滚动
`S-SPC` | 向上滚动
`n` | 跳转到下一小节
`p` | 跳转到上一小节
`C-c C-y` | 跳转到 ess
`C-c C-z` | 跳转到 ess 的命令行末端
`s` | prefix command, 跳转

-------------------------------------------------------------------------------

0 .. 9          digit-argument
C-c             Prefix Command
ESC             Prefix Command
-               negative-argument
/               isearch-forward
0 .. 9          digit-argument

a | ess-display-help-apropos
h | ess-display-help-on-object
i | ess-display-package-index
v | ess-display-vignettes
w | ess-display-help-in-browser

f               ess-eval-function-or-paragraph-and-step
l               ess-eval-line-and-step
r               ess-eval-region-and-go
<C-return>      ess-eval-region-or-line-and-step

g               revert-buffer
q               quit-window
k               kill-this-buffer
?               ess-describe-help-mode
x               ess-kill-buffer-and-go

s               Prefix Command
<remap>         Prefix Command

C-c C-c         ess-eval-region-or-function-or-paragraph-and-step
C-c C-d         ess-doc-map
C-c C-e         ess-extra-map

C-c C-f         ess-eval-function
C-c C-j         ess-eval-line
C-c C-n         ess-eval-line-and-step
C-c C-r         ess-eval-region

C-c C-k         ess-request-a-process
C-c C-l         ess-load-file

C-c C-s         ess-switch-process
C-c C-t         ess-dev-map
C-c C-v         ess-display-help-on-object

C-c ESC         Prefix Command
C-c h           ess-handy-commands

C-M-a           ess-goto-beginning-of-function-or-para
C-M-e           ess-goto-end-of-function-or-para
C-M-x           ess-eval-function

s <             beginning-of-buffer
s >             end-of-buffer
s ?             ess-describe-sec-map
s D             ess-skip-to-help-section
s a             ess-skip-to-help-section
s d .. s e      ess-skip-to-help-section
s n             ess-skip-to-help-section
s r .. s v      ess-skip-to-help-section

C-c C-t C-b     ess-bp-set
C-c C-t C-d     ess-debug-flag-for-debugging
C-c C-t C-e     ess-debug-toggle-error-action
C-c C-t C-k     ess-bp-kill-all
C-c C-t C-l     ess-bp-set-logger
C-c C-t C-n     ess-bp-next
C-c C-t C-o     ess-bp-toggle-state
C-c C-t C-p     ess-bp-previous
C-c C-t C-s     ess-r-set-evaluation-env
C-c C-t C-u     ess-debug-unflag-for-debugging
C-c C-t C-w     ess-watch
C-c C-t 0 .. C-c C-t 9          ess-electric-selection
C-c C-t ?       ess-tracebug-show-help
C-c C-t B       ess-bp-set-conditional
C-c C-t I       ess-debug-goto-input-event-marker
C-c C-t K       ess-bp-kill-all
C-c C-t L       ess-bp-set-logger
C-c C-t T       ess-toggle-tracebug
C-c C-t `       ess-show-traceback
C-c C-t b       ess-bp-set
C-c C-t d       ess-debug-flag-for-debugging
C-c C-t e       ess-debug-toggle-error-action
C-c C-t i       ess-debug-goto-input-event-marker
C-c C-t k       ess-bp-kill
C-c C-t l       ess-r-devtools-load-package
C-c C-t n       ess-bp-next
C-c C-t o       ess-bp-toggle-state
C-c C-t p       ess-bp-previous
C-c C-t s       ess-r-set-evaluation-env
C-c C-t u       ess-debug-unflag-for-debugging
C-c C-t w       ess-watch
C-c C-t ~       ess-show-call-stack
C-c C-t C-S-b   ess-bp-set-conditional
C-c C-t C-S-d   ess-debug-unflag-for-debugging

C-c C-e C-d     ess-dump-object-into-edit-buffer
C-c C-e C-e     ess-execute
C-c C-e TAB     ess-install-library
C-c C-e C-l     ess-load-library
C-c C-e C-s     ess-set-style
C-c C-e C-t     ess-build-tags-for-directory
C-c C-e C-w     ess-execute-screen-options
C-c C-e /       ess-set-working-directory
C-c C-e d       ess-dump-object-into-edit-buffer
C-c C-e e       ess-execute
C-c C-e i       ess-install-library
C-c C-e l       ess-load-library
C-c C-e s       ess-set-style
C-c C-e t       ess-build-tags-for-directory
C-c C-e w       ess-execute-screen-options

C-c C-d C-a     ess-display-help-apropos
C-c C-d C-d     ess-display-help-on-object
C-c C-d C-e     ess-describe-object-at-point
C-c C-d TAB     ess-display-package-index
C-c C-d RET     ess-manual-lookup
C-c C-d C-o     ess-display-demos
C-c C-d C-r     ess-reference-lookup
C-c C-d C-v     ess-display-vignettes
C-c C-d C-w     ess-help-web-search
C-c C-d a       ess-display-help-apropos
C-c C-d d       ess-display-help-on-object
C-c C-d e       ess-describe-object-at-point
C-c C-d i       ess-display-package-index
C-c C-d m       ess-manual-lookup
C-c C-d o       ess-display-demos
C-c C-d r       ess-reference-lookup
C-c C-d v       ess-display-vignettes
C-c C-d w       ess-help-web-search

C-c M-f         ess-eval-function-and-go
C-c M-j         ess-eval-line-and-go
C-c M-l         ess-load-file
C-c M-r         ess-eval-region-and-g

# dired-mode #

用于编辑文件和路径列表的主要编辑模式（Major mode）。

键前缀

key | bindings
:-----|:--------
`%` | 高级正则表达式操作
`*` | 高级选中操作
`:` | 加密验证操作

shell命令

 Key | binding
:-----|:--------
`!`/`X` | dired-do-shell-command 执行shell命令
`&` | dired-do-async-shell-command 异步执行shell命令
`A` | dired-do-find-regexp 正则表达式查找
`Q` | dired-do-find-regexp-and-replace
`B` | dired-do-byte-compile 字节编译
`C` | dired-do-copy 复制
`D` | dired-do-delete 删除
`H` | dired-do-hardlink 硬链接
`S` | dired-do-symlink
`L` | dired-do-load 加载
`M` | dired-do-chmod
`O` | dired-do-chown
`G` | dired-do-chgrp
`P` | dired-do-print
`R` | dired-do-rename
`T` | dired-do-touch
`Z` | dired-do-compress 压缩
`c` | dired-do-compress-to 压缩至...
`k` | dired-do-kill-lines 删除行
`l` | dired-do-redisplay 重新显示
`x` | dired-do-flagged-delete 删除标记的项目

对文件的操作

 Key | binding
:-----|:--------
`W` | browse-url-of-dired-file 使用外部应用打开文件
`a` | dired-find-alternate-file 打开替代文件（默认关闭）
`j` | dired-goto-file 去往文件
`o` | dired-find-file-other-window 从另一窗口打开
`v` | dired-view-file 阅读文件（只读）
`C-o` | dired-display-file 显示文件内容（只读）
`RET`/`e`/`f` | dired-find-file 打开文件（可写）
`y` | dired-show-file-type 显示文件类型
`w` | dired-copy-filename-as-kill 复制文件名
`s` | dired-sort-toggle-or-edit 排序
`=` | dired-diff 比较差异
`#` | dired-flag-auto-save-files 标记自动保存文件

对路径的操作

 Key | binding
:-----|:--------
`$` | dired-hide-subdir 隐藏子路径
`M-$` | dired-hide-all 隐藏所有子路径
`+` | dired-create-directory 新创建路径
`i` | dired-maybe-insert-subdir 在当前窗口打开子路径
`.` | dired-clean-directory 清理路径

标记与取消标记

 Key | binding
:-----|:--------
`d` | dired-flag-file-deletion 标记要删除的对象
`m` | dired-mark 选中
`u` | dired-unmark 取消选中
`M-{` | dired-prev-marked-file 上一个选中
`M-}` | dired-next-marked-file 下一个选中
`U`/`M-DEL` | dired-unmark-all-marks 全部取消选中
`DEL` | dired-unmark-backward 退回取消选中
`t` | dired-toggle-marks 选中取反
`~` | dired-flag-backup-files 标记备份文件

导航快捷键

 Key | binding
:-----|:--------
`SPC`/`n` | dired-next-line 下一行
`S-SPC`/`p` | dired-previous-line 上一行
`<` | dired-prev-dirline 上一行文件路径
`>` | dired-next-dirline 下一行文件路径
`^` | dired-up-directory 上一页路径
`?` | dired-summary 文件路径总结
`C-M-d` | dired-tree-down 下一级文件树
`C-M-u` | dired-tree-up 上一级文件树
`C-M-n` | dired-next-subdir 下一个子路径
`C-M-p` | dired-prev-subdir 上一个子路径

其他

 Key | binding
:-----|:------
`g` | revert-buffer 重载/更新
`h` | describe-mode 打开模式文档
`q` | quit-window 推出窗口
`(` | dired-hide-details-mode 细节隐藏模式切换

# evil-mode

## evil-window-map

Keymap for window-related commands.

key | binding
:---|:-------
C-b    | evil-window-bottom-right
C-c    | evil-window-delete
C-f    | ffap-other-window
C-n    | evil-window-new
C-o    | delete-other-windows
C-p    | evil-window-mru
C-r    | evil-window-rotate-downwards

C-s    | evil-window-split
C-v    | evil-window-vsplit

C-t    | evil-window-top-left

C-w    | evil-window-next
C-_    | evil-window-set-height
+      | evil-window-increase-height
-      | evil-window-decrease-height
<      | evil-window-decrease-width
=      | balance-windows
>      | evil-window-increase-width
H      | evil-window-move-far-left
J      | evil-window-move-very-bottom
K      | evil-window-move-very-top
L      | evil-window-move-far-right
R      | evil-window-rotate-upwards
S      | evil-window-split
W      | evil-window-prev
_      | evil-window-set-height
b      | evil-window-bottom-right
c      | evil-window-delete
h      | evil-window-left
j      | evil-window-down
k      | evil-window-up
l      | evil-window-right
n      | evil-window-new
o      | delete-other-windows
p      | evil-window-mru
r      | evil-window-rotate-downwards
s      | evil-window-split
t      | evil-window-top-left
v      | evil-window-vsplit
w      | evil-window-next
| | evil-window-set-width
C-S-h  | evil-window-move-far-left
C-S-j  | evil-window-move-very-bottom
C-S-k  | evil-window-move-very-top
C-S-l  | evil-window-move-far-right
C-S-r  | evil-window-rotate-upwards
C-S-s  | evil-window-split
C-S-w  | evil-window-prev

## evil-insert-state-map

Keymap for Insert state.

key | binding
:---|:-------
C-a  | evil-paste-last-insertion
C-d  | evil-shift-left-line
C-e  | evil-copy-from-below
C-k  | evil-insert-digraph
C-n  | evil-complete-next
C-o  | evil-execute-in-normal-state
C-p  | evil-complete-previous
C-r  | evil-paste-from-register
C-t  | evil-shift-right-line
C-v  | quoted-insert
C-w  | evil-delete-backward-word
C-y  | evil-copy-from-above
C-z  | evil-emacs-state
<delete>  | delete-char
<escape>  | evil-normal-state
<mouse-2> | mouse-yank-primary

## evil-motion-state-map

Keymap for Motion state.

key | binding
:---|:-------
h/l | evil-backward/forward-char 向后/前移动一个字符
j/k | evil-next/previous-line 想下/上移动一行
B/W | evil-backward/forward-WORD-begin 向后/前移动到 WORD 前
E | evil-forward-WORD-end 向前移动到 WORD 后
w | evil-forward-word-begin 向前移动到 word 前
C-b/C-f | evil-scroll-page-up/down 向上/下滚动页面
C-d | evil-scroll-down 向下滚动
C-y/C-e | evil-scroll-line-up/down 向上/下滚动一行
TAB/C-o | evil-jump-forward/backward 前/后跳
RET |  evil-ret
C-z |  evil-emacs-state 切换 emacs 和 vim 模式
C-v |  evil-visual-block
C-w |  evil-window-map
C-] |  evil-jump-to-tag
`%` |  evil-jump-item
C-^ |  evil-buffer
SPC |  evil-forward-char
`!` | evil-shell-command
`#` |  evil-search-word-backward
`$` |    evil-end-of-line
`'` |    evil-goto-mark-line
``` |    evil-goto-mark
`G` |    evil-goto-line

( |    evil-backward-sentence-begin
) |    evil-forward-sentence-begin

K |    evil-lookup
* |    evil-search-word-forward
`/`/`?` |    evil-search-forward/backward
N/n |    evil-search-previous/next
, |    evil-repeat-find-char-reverse
; |    evil-repeat-find-char
F |    evil-find-char-backward
T |    evil-find-char-to-backward

+ |    evil-next-line-first-non-blank
- |    evil-previous-line-first-non-blank

0 |    evil-digit-argument-or-evil-beginning-of-line
1 .. 9  | digit-argument
: |    evil-ex

H |    evil-window-top
L |    evil-window-bottom
M |    evil-window-middle

V |    evil-visual-line

Y |    evil-yank-line
y |    evil-yank

[ |    Prefix Command
\ |    evil-execute-in-emacs-state
] |    Prefix Command
^ |    evil-first-non-blank
_ |    evil-next-line-1-first-non-blank

`|` |    evil-goto-column
b |    evil-backward-word-begin
e |    evil-forward-word-end
f |    evil-find-char
g |    Prefix Command

t |    evil-find-char-to
v |    evil-visual-char

z |    Prefix Command
`{` |    evil-backward-paragraph

`}` |    evil-forward-paragraph
C-6 |  evil-switch-to-windows-last-buffer
<down> | evil-next-line
<down-mouse-1>  | evil-mouse-drag-region
<left> | evil-backward-char
<remap> | Prefix Command
<right> | evil-forward-char
<up> | evil-previous-line

<remap> <ace-jump-char-mode>    evil-ace-jump-char-mode
<remap> <ace-jump-line-mode>    evil-ace-jump-line-mode
<remap> <ace-jump-word-mode>    evil-ace-jump-word-mode
<remap> <avy-goto-char>         evil-avy-goto-char
<remap> <avy-goto-char-2>       evil-avy-goto-char-2
<remap> <avy-goto-char-2-above> evil-avy-goto-char-2-above
<remap> <avy-goto-char-2-below> evil-avy-goto-char-2-below
<remap> <avy-goto-char-in-line> evil-avy-goto-char-in-line
<remap> <avy-goto-line>         evil-avy-goto-line
<remap> <avy-goto-subword-0>    evil-avy-goto-subword-0
<remap> <avy-goto-subword-1>    evil-avy-goto-subword-1
<remap> <avy-goto-word-0>       evil-avy-goto-word-0
<remap> <avy-goto-word-1>       evil-avy-goto-word-1
<remap> <avy-goto-word-1-above> evil-avy-goto-word-1-above
<remap> <avy-goto-word-1-below> evil-avy-goto-word-1-below
<remap> <avy-goto-word-or-subword-1> evil-avy-goto-word-or-subword-1

z RET | Keyboard Macro
z + |  evil-scroll-bottom-line-to-top
z - |  Keyboard Macro
z . |  Keyboard Macro
z H |  evil-scroll-left
z L |  evil-scroll-right
z ^ |  evil-scroll-top-line-to-bottom
z b |  evil-scroll-line-to-bottom
z h |  evil-scroll-column-left
z l |  evil-scroll-column-right
z t |  evil-scroll-line-to-top
z z |  evil-scroll-line-to-center
z <left>  | Keyboard Macro
z <return> | Keyboard Macro
z <right> | Keyboard Macro

C-w C-b |  evil-window-bottom-right
C-w C-c |  evil-window-delete
C-w C-f |  ffap-other-window
C-w C-n |  evil-window-new
C-w C-o |  delete-other-windows
C-w C-p |  evil-window-mru
C-w C-r |  evil-window-rotate-downwards
C-w C-s |  evil-window-split
C-w C-t |  evil-window-top-left
C-w C-v |  evil-window-vsplit
C-w C-w |  evil-window-next
C-w C-_ |  evil-window-set-height
C-w + | evil-window-increase-height
C-w - | evil-window-decrease-height
C-w < | evil-window-decrease-width
C-w = | balance-windows
C-w > | evil-window-increase-width
C-w H | evil-window-move-far-left
C-w J | evil-window-move-very-bottom
C-w K | evil-window-move-very-top
C-w L | evil-window-move-far-right
C-w R | evil-window-rotate-upwards
C-w S | evil-window-split
C-w W | evil-window-prev
C-w _ | evil-window-set-height
C-w b | evil-window-bottom-right
C-w c | evil-window-delete
C-w h | evil-window-left
C-w j | evil-window-down
C-w k | evil-window-up
C-w l | evil-window-right
C-w n | evil-window-new
C-w o | delete-other-windows
C-w p | evil-window-mru
C-w r | evil-window-rotate-downwards
C-w s | evil-window-split
C-w t | evil-window-top-left
C-w v | evil-window-vsplit
C-w w | evil-window-next
C-w | | evil-window-set-width
C-w C-S-h | evil-window-move-far-left
C-w C-S-j |  evil-window-move-very-bottom
C-w C-S-k |  evil-window-move-very-top
C-w C-S-l |  evil-window-move-far-right
C-w C-S-r |  evil-window-rotate-upwards
C-w C-S-s |  evil-window-split
C-w C-S-w |  evil-window-prev

[ ( |   evil-previous-open-paren
[ [ |   evil-backward-section-begin
[ ] |   evil-backward-section-end
[ { |   evil-previous-open-brace

] ) |   evil-next-close-paren
] [ |   evil-forward-section-end
] ] |   evil-forward-section-begin
] } |   evil-next-close-brace

g C-] | find-tag
g # |   evil-search-unbounded-word-backward
g $ |   evil-end-of-visual-line
g * |   evil-search-unbounded-word-forward
g 0 |   evil-beginning-of-visual-line
g E |   evil-backward-WORD-end
g N |   evil-previous-match
g ^ |   evil-first-non-blank-of-visual-line
g _ |   evil-last-non-blank
g d |   evil-goto-definition
g e |   evil-backward-word-end
g g |   evil-goto-first-line
g j |   evil-next-visual-line
g k |   evil-previous-visual-line
g m |   evil-middle-of-visual-line
g n |   evil-next-match
g v |   evil-visual-restore

# 学习

[emacs lisp 风格指南](https://github.com/emacs-china/emacs-lisp-style-guide/blob/master/README-zhCN.md)

# 常用包

## 外观

正在使用
[solarized-theme](https://github.com/bbatsov/solarized-emacs)
[smart-mode-line](https://github.com/Malabarba/smart-mode-line/)
[golden-ratio](https://github.com/roman/golden-ratio.el) 自动调整 window 的大小比例，将当前活动 buffer 所在的 window 调大，非活动窗口调小。

以前用过
[monokai-theme](https://github.com/oneKelvinSmith/monokai-emacs) 对比度有些高不太适应，后来改为了 solarized-theme。
[moe-theme](https://github.com/kuanyui/moe-theme.el)
[powerline]
[spaceline]
