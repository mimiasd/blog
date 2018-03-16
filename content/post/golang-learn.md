---
title: "Golang Learning"
date: 2018-03-13T17:56:13+08:00
lastmod: 2018-03-13T17:56:13+08:00
draft: false
keywords: [go,learn]
description: ""
tags: [go,learn]
categories: [golang]
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

# Foundational Golang 

- [A Tour of Go](https://tour.golang.org/welcome/1)

- [How to Write Go Code](https://golang.org/doc/code.html) 

- [The Go Programming Language Specification](https://golang.org/ref/spec)

- [Effective Go](https://golang.org/doc/effective_go.html)

## Golang Tools

- [Go Tools](https://golang.org/cmd/go/)

## Golang Dianostics

- [Diagnostics](https://golang.org/doc/diagnostics.html)

- [delve](https://github.com/derekparker/delve)

- [gdb](https://www.gnu.org/software/gdb/)

## Golang FAQ

- [Frequently Asked Questions (FAQ)](https://golang.org/doc/faq)

## Golang Wiki

- [Wiki](https://github.com/golang/go/wiki)

# Advanced Golang

## Go's Assembler

### [A Quick Guide to Go's Assembler](https://golang.org/doc/asm)

- GOOS=linux GOARCH=amd64 go tool compile -S x.go        # or: go build -gcflags -S x.go

- The FUNCDATA and PCDATA directives contain information for use by the garbage collector;

- There are four predeclared symbols that refer to pseudo-registers.
  - FP: Frame pointer: arguments and locals.
  - PC: Program counter: jumps and branches.
  - SB: Static base pointer: global symbols.
  - SP: Stack pointer: top of stack.

### [Chapter I: A Primer on Go Assembly](https://github.com/teh-cmc/go-internals/tree/master/chapter1_assembly_primer)
