---
title: "Go Commands"
date: 2018-03-14T15:46:48+08:00
lastmod: 2018-03-14T15:46:48+08:00
draft: false
keywords: [go,command]
description: ""
tags: [go,command]
categories: [go]
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

# go build

　　通过依赖和导入路径的名字来构建编译包，但不会安装结果。

　　如果构建的参数是一系列的 `.go` 文件，那么 build 是把它们当做单个包的源文件。

　　当编译一个单独的 main 包时，build 把结果的可执行文件输出为第一个源文件命名的输出文件。

　　当编译多个包时或者一个单独的非 main 包时，build 编译这些包，但丢弃掉结果内容，只是用来检测这些包是否能够被编译。

　　当编译包时， build 忽略那些 "_test.go" 结尾的文件。

　　'-o' 参数只允许编译单个包，强制 build 把结果可执行文件或对象命名为该命名的输出文件，而不是默认的行为。
