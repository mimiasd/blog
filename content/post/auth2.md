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

> [OAuth2.0 RFC](https://tools.ietf.org/html/rfc6749)

# 1. 简介

　　传统客户端-服务端认证模型中，是客户端用资源拥有者的证书去访问受限资源。而当资源拥有者把证书给第三方应用时，会出现以下问题和限制：

- 第三方应用要求储存该证书，以备后用，通常是一个明文密码。

- 服务端需要支持密码认证，而密码认证的方式在安全方面存在与生俱来的缺点。

- 第三方应用获得了过大的权限，导致资源拥有者无法限制首先资源的子集。

- 资源拥有者不能撤回单个第三方应用，只能通过改变第三方应用的密码，收回所有第三方应用的权限。

- 妥协任何第三方应用，就会给这个第三方应用的终端用户密码，以及密码关联的所有受保护资源。

　　OAuth 引入了授权层，把资源所有者和客户端角色分开，来解决上面的问题。在 OAuth 中，客户端请求服务端的受限资源，并且被发一系列不同于资源拥有者的证书。  

　　客户端获得一个表示特定范围、生命周期和其他访问属性的字符串 - `token`，来代替直接使用资源拥有者的证书，访问受限资源。资源访问者允许后，通过授权服务器发放令牌给第三方客户端。客户端利用这个令牌来访问受限资源。  

　　例如，一个终端用户(资源拥有者)，可以授予一个打印服务(客户端)存储在相片分享服务器(资源服务器)上到受保护的照片，而不用把她的帐号和密码告诉打印服务。作为代替，她直接授权给被相片分享服务(认证服务器)信任的服务，认证服务器将分发特殊指派的证书(访问令牌)给打印服务器。  

　　该说明书用于 HTTP。基于其他协议的 OAuth，不在该说明书讨论范围内。

# 1.1 角色

  OAuth 定义了四个角色：

- 资源拥有者(resource owner)
  - 有能力授予一个受限资源访问权限的实体。当资源拥有者是一个人时，它指代一个终端用户。

- 资源服务器(resource server)
  - 储存着受保护资源的服务，有能力接收和响应，使用访问令牌的受保护资源请求。

- 客户端(client)
  - 通过资源拥有者授权，代表资源拥有者发出对受限资源请求的一个应用。术语 "client" 不表示任何特殊的实现特性(例如：不管这个应用运行在服务器，桌面环境，或者其他设备上)。

- 授权服务器(authorization server)
  - 在成功鉴定资源拥有者，并获得其授权后，授权服务发布访问令牌给客户端。
