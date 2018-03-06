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

# 安装的各类插件

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

## nerdtree-git-plugin

　　安装 [nerdtree-git-plugin](https://github.com/Xuyuanp/nerdtree-git-plugin)：

```
1. Add Plugin 'Xuyuanp/nerdtree-git-plugin' to your vimrc file.
2. Reload your vimrc or restart
3. Run :BundleInstall
``` 

　　这是一个开箱即用的插件， 显示的符号配置如下：

```vimscript
let g:NERDTreeIndicatorMapCustom = {
    \ "Modified"  : "✹",
    \ "Staged"    : "✚",
    \ "Untracked" : "✭",
    \ "Renamed"   : "➜",
    \ "Unmerged"  : "═",
    \ "Deleted"   : "✖",
    \ "Dirty"     : "✗",
    \ "Clean"     : "✔︎",
    \ 'Ignored'   : '☒',
    \ "Unknown"   : "?"
    \ }
 ```

## nerd-commenter

　　安装 [nerd-commenter](https://github.com/scrooloose/nerdcommenter)：

```
1. Add Plugin 'scrooloose/nerdcommenter' to your vimrc file.
2. Reload your vimrc or restart
3. Run :BundleInstall
```
　　默认配置如下：

```  
<leader>cc   加注释
<leader>cu   解开注释

<leader>c<space>  加上/解开注释, 智能判断
<leader>cy        先复制, 再注解(p可以进行黏贴)
```

　　最终配置：

```
Bundle 'scrooloose/nerdcommenter'

" 注释的时候自动加个空格, 强迫症必配
let g:NERDSpaceDelims = 1
```

## fzf

　　安装 [fzf](https://github.com/junegunn/fzf.vim)来代替[ctrlp](https://github.com/ctrlpvim/ctrlp.vim)，以此实现与 shell 终端的通用，可以参考[fzf.vim 用法](https://blog.zfanw.com/fzf-vim-usage/)：

```
Bundle 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' } 
Bundle 'junegunn/fzf.vim'
```

　　进行如下按键映射：

```
nnoremap <silent> <C-p> :Files<CR>
```

### 常用操作

- `Files [PATH]`：在 `PATH` 目录下进行查找，当前目录被映射成快捷键`<Ctrl-P>`。

## ack

　　安装 [ack.vim](https://github.com/mileszs/ack.vim)：

```
Bunlde 'mileszs/ack.vim'
```

　　进行如下按键映射：

```
map <leader>a :Ack<space>
```

### 常用操作

- `:Ack [options] {pattern} [{directories}]`：在指定目录下进行查找匹配的行。

## vim-surround

　　安装 [vim-surround](https//github.com/tpope/vim-surround)：

```
git clone git://github.com/tpope/vim-surround.git ~/.vim/bundle
```

### 常用操作

- `cs"'` 或 `cs"<q>`：意味着`change sourroundings " to '`，例如把：`"Hello world!"` 变为 `'Hello world!'` 或 `<q>Hello world!</q>`。

- `cst"`： 意味着 `change sourroundings tag to "`，例如把 `<q>Hello world!</q>` 变为 `"Hello world!"`。

- `ds"`：意味着 `delete sourroundings "`，例如把 `"Hello world!"` 变为 `Hello world!`。

- `ysiw]`：意味着 `you surround in word ]`，例如把 `Hello world!` 变为 `[Hello] world!`。

- `csw"`：意味着 `you surround word "`，例如把 `Hello world!` 变为 `"Hello" world!`。

- `yss`：意味着 `you surround surroundings )`，例如把 `{Hello} world!` 变为 `({Hello} world!)`。

## vim-repeat

　　安装 [vim-repeat](https://github.com/tpope/vim-repeat)：

```
Bundle 'tpope/vim-repeat'
```
 
　　按 "." 键重复上次的操作。

## vim-airline

　　安装 [vim-airline](https://github.com/vim-airline/vim-airline)：

```
Plugin 'vim-airline/vim-airline'
Plugin 'vim-airline/vim-airline-themes'
```
　　配置如下：

```
Bundle 'vim-airline/vim-airline'

if !exists('g:airline_symbols')
  let g:airline_symbols = {}
endif

let g:airline_left_sep = '▶'
let g:airline_left_alt_sep = '❯'
let g:airline_right_sep = '◀'
let g:airline_right_alt_sep = '❮'
let g:airline_symbols.linenr = '¶'
let g:airline_symbols.branch = '⎇'

" 是否打开tabline
let g:airline#extensions#tabline#enabled = 1

" 这个是安装字体后 必须设置此项"
let g:airline_powerline_fonts = 1

" 设置切换Buffer快捷键"
 nnoremap <leader><left> :bp<CR>
 nnoremap <leader><right> :bn<CR>
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
 配置如下：

```
nmap tb :TagbarToggle<CR>

" 启动时自动focus
let g:tagbar_autofocus = 1

" gotags 配置
let g:tagbar_type_go = {
    \ 'ctagstype': 'go',
    \ 'kinds' : [
        \'p:package',
        \'f:function',
        \'v:variables',
        \'t:type',
        \'c:const'
    \]
\}
```

## vim-easymotion

　　安装 [vim-easymotion](https://github.com/easymotion/vim-easymotion)：

```
Plugin 'easymotion/vim-easymotion'
```

 配置如下：

```
map <leader> <Plug>(easymotion-prefix)
```

## vim-colors-solarized

 安装 [vim-colors-solarized](https://github.com/altercation/vim-colors-solarized)：

```
Plugin 'altercation/vim-colors-solarized'

cd vim-colors-solarized/colors
mv solarized.vim ~/.vim/colors/
```

## rainbow

 安装 [rainbow](https://github.com/luochen1990/rainbow)：

```
Plugin "luochen1990/rainbow"
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







## tabular

 安装 [tabular](https://github.com/godlygeek/tabular)：

```
Plugin 'godlygeek/tabular'
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

./install.py --clang-completer --go-completer --js-completer
```

 当安装完成后打开 vim，可能出现以下错误：

> ImportError: libtinfo.so.5 no exsit

 解决方法是：

> ln -s /lib64/libncurses.so.5 /lib64/libtinfo.so.5

# 常见问题

1. 问题1：当修改 leader 键为空格键后，普通空格按键会有一定延迟。

- 解决办法：[参考"vim let mapleader = “\<Space>” annoying cursor movement"](https://stackoverflow.com/questions/25341062/vim-let-mapleader-space-annoying-cursor-movement)。

