---
title: "Auth2.0"
date: 2018-02-28T17:59:26+08:00
lastmod: 2018-02-28T17:59:26+08:00
draft: false
keywords: [auth2]
description: ""
tags: [auth]
categories: [auth]
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

# 简介

　　传统客户端-服务端认证模型中，是客户端用资源拥有者的证书去访问受限资源。而当资源拥有者把证书给第三方应用时，会出现以下问题和限制：

- 第三方应用要求储存该证书，以备后用，通常是一个明文密码。

- 服务端需要支持密码认证，而密码认证的方式在安全方面存在与生俱来的缺点。

- 第三方应用获得了过大的权限，导致资源拥有者无法限制首先资源的子集。

- 资源拥有者不能撤回单个第三方应用，只能通过改变第三方应用的密码，收回所有第三方应用的权限。

- 妥协任何第三方应用，就会给这个第三方应用的终端用户密码，以及密码关联的所有受保护资源。

　　OAuth 引入了授权层，把资源所有者和客户端角色分开，来解决上面的问题。在 OAuth 中，客户端请求服务端的受限资源，并且被发一系列不同于资源拥有者的证书。

 客户端获得一个表示特定范围、生命周期和其他访问属性的字符串 - `token`，来代替直接使用资源拥有者的证书，访问受限资源。资源访问者允许后，通过授权服务器发放令牌给第三方客户端。客户端利用这个令牌来访问受限资源。
