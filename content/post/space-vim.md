---
title: "Space Vim"
date: 2018-03-04T18:06:56+08:00
lastmod: 2018-03-04T18:06:56+08:00
draft: false
keywords: []
description: "这篇文章主要介绍space-vim的安装"
tags: [vim, editor]
categories: [space-vim]
author: "mimiasd"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
# comment: false
# toc: true
# autoCollapseToc: false
# postMetaInFooter: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
# reward: false
# mathjax: false
mathjaxEnableSingleDollar: false
---

> 这篇文章主要介绍[`space-vim`](https://github.com/liuchengxu/space-vim)的安装

# vim 安装

 对于 vim 的安装，我一般选择源码安装在`/usr/local/`目录下

## 安装依赖包

 vim 安装时可能依赖于以下包：

> libncurses5-dev libgnome2-dev libgnomeui-dev libgtk2.0-dev libatk1.0-dev libbonoboui2-dev libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev python3-dev ruby-dev lua5.1 lua5.1-dev git

## 开始安装

 从 github 上下载 vim 的 master 分支：

```
cd /usr/local && wget https://github.com/vim/vim/archive/master.zip
```

 解压 master.zip，并进入 src 目录：

```
unzip master.zip && cd vim-master/src
```

 配置 vim 支持的特性：

```
./configure --with-features=huge \
            -enable-multibyte \
            -enable-rubyinterp \
            -enable-pythoninterp \
            -with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu \
            -enable-perlinterp \
            -enable-luainterp \
            -enable-cscope
```

 然后编译安装：

```
make && make install
```

# space-vim 安装

## 安装 space-vim

```
bash <(curl -fsSL https://git.io/vFUhE) 
``` 

## 安装字体

 下载 [powerline fonts](https://github.com/powerline/fonts) 字体：

```
git clone https://github.com/powerline/fonts.git ~/.fonts
sh ~/.fonts/install.sh
```

 powerline font 安装完成后，在 .spacevim 中启用字体：

```
let g:airline_powerline_fonts=1
```
