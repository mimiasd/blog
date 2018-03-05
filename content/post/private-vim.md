---
title: "Private Vim"
date: 2018-03-04T20:29:45+08:00
lastmod: 2018-03-04T20:29:45+08:00
draft: false
keywords: []
description: ""
tags: [editor, vim]
categories: [vim]
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

# 概述

　　这是我个人的 vim 配置过程。

　　对于 vimscript，可以参考[使用脚本编写 Vim 编辑器](https://www.ibm.com/developerworks/cn/linux/l-vim-script-1/index.html?ca=drs-)和 [Vimscript 编程指南](https://www.gitbook.com/book/kenvifire/vimscript/details)。

> 下面是各个插件的安装。

## Vundle

　　首先安装 vim 插件管理器 [Vundle](https://github.com/VundleVim/Vundle.vim)：

```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

　　然后在 `.vimrc` 中添加下面的 Vundle 配置：

```
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
" call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
" filetype plugin on

" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
```

## nerdtree

　　安装 [nerdtree](https://github.com/scrooloose/nerdtree)：

```
git clone https://github.com/scrooloose/nerdtree.git ~/.vim/bundle/nerdtree
``` 

### 简介
 
　　nerdtree 是一个文件系统探测器。通过这个插件，用户可以形象地浏览复杂的文件层次结构，快速打开文件浏览或编辑，以及进行基础的文件系统操作。

　　具体可以参考[Aaron 的 nerdtree 配置](http://aaronmoment.cn/nerdtree/)以及[如何优雅地使用 VIM 文件管理插件](https://linux.cn/article-7424-1.html)。

### 常用操作

- `<Ctrl-e>`：切换显示 NERDtree。

- `<Ctrl-w>方向键`：切换窗口。

- `<leader>e`：在 NERDtree 中找到当前文件的位置。

- `:Bookmark [<name>]`：在当前目录或文件创建书签。

- `:ClearBookmarks [<name>] 或 D`：删除相应书签。

- `o 或 <Enter>`：打开文件、目录和书签。

- `i`：竖屏分割打开一个新的文件窗口。

- `s`：横屏分割打开一个新的文件窗口。

- `P`：跳到根节点。

- `m`：显示 NERD 树目录。

- `I`：显示隐藏文件开关。

- `B`：显示书签开关。

## nerd-commenter

 安装 [nerd-commenter](https://github.com/scrooloose/nerdcommenter)：

```
1. Add Plugin 'scrooloose/nerdcommenter' to your vimrc file.
2. Reload your vimrc or restart
3. Run :BundleInstall
```

## ultisnips

 安装 [ultisnips](https://github.com/SirVer/ultisnips)：

```
" Track the engine.
Plugin 'SirVer/ultisnips'

" Snippets are separated from the engine. Add this if you want them:
Plugin 'honza/vim-snippets'

" Trigger configuration. Do not use <tab> if you use https://github.com/Valloric/YouCompleteMe.
let g:UltiSnipsExpandTrigger="<tab>"
let g:UltiSnipsJumpForwardTrigger="<c-b>"
let g:UltiSnipsJumpBackwardTrigger="<c-z>"

" If you want :UltiSnipsEdit to split your window.
let g:UltiSnipsEditSplit="vertical"
```

## ctrlp

 安装 [ctrlp](https://github.com/ctrlpvim/ctrlp.vim)：

```
1. Add Plugin 'ctrlpvim/ctrlp.vim' to your vimrc file.
2. Reload your vimrc or restart
3. Run :BundleInstall
```

## vim-surround

 安装 [vim-surround](https//github.com/tpope/vim-surround)：

```
git clone git://github.com/tpope/vim-surround.git ~/.vim/bundle
```

## vim-airline

 安装 [vim-airline](https://github.com/vim-airline/vim-airline)：

```
Plugin 'vim-airline/vim-airline'
Plugin 'vim-airline/vim-airline-themes'
```

## ctags

 安装 [ctags](https://github.com/vim-scripts/ctags.vim)：

```
Plugin 'vim-scripts/ctags.vim'
```

## tagbar

 安装 [tagbar](https://github.com/majutsushi/tagbar)：

```
Plugin 'majutsushi/tagbar'
```

## vim-easymotion

 安装 [vim-easymotion](https://github.com/easymotion/vim-easymotion)：

```
Plugin 'easymotion/vim-easymotion'
```

## vim-colors-solarized

 安装 [vim-colors-solarized](https://github.com/altercation/vim-colors-solarized)：

```
Plugin 'altercation/vim-colors-solarized'
```

## tabular

 安装 [tabular](https://github.com/godlygeek/tabular)：

```
Plugin 'godlygeek/tabular'
```

## rainbow

 安装 [rainbow](https://github.com/luochen1990/rainbow)：

```
Plugin "luochen1990/rainbow"
```

## emmet-vim

 安装 [emmet-vim](https://github.com/mattn/emmet-vim)：

```
Plugin 'mattn/emmet-vim'
```

## vim-indent-guides

 安装 [vim-indent-guides](https://github.com/nathanaelkane/vim-indent-guides)：

```
Plugin 'nathanaelkane/vim-indent-guides'
```

## vim-go

 安装 [vim-go](https://github.com/fatih/vim-go)：

```
Plugin 'fatih/vim-go'
```

## gocode

 安装 [gocode](https://github.com/nsf/gocode)：

```
Plugin 'nsf/gocode', {'rtp': 'vim/'}
```

## YouCompleteMe

 安装 [YouCompleteMe](https://github.com/Valloric/YouCompleteMe)：

```
git clone git://github.com/Valloric/YouCompleteMe.git ~/.vim/bundle

cd ~/.vim/bundle/YouCompleteMe

git submodule update --init --recursive 

./install.py --all
```
