---
title: "Jwt"
date: 2018-03-09T18:00:33+08:00
lastmod: 2018-03-09T18:00:33+08:00
draft: false
keywords: [jwt]
description: ""
tags: [jwt]
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

> [JWT RFC](https://tools.ietf.org/html/rfc7519)

# JWT

　　JSON Web Token(JWT) 是一个紧凑的，URL 安全的代表在两部分传输要求描述。JWT 中的要求被编码到一个 JSON 对象中，被用作一个 JSON 网络签名(JWS)的负载，或者 JSON 网络加密结构中的文本，通过数字签名或完整的信息授权码或加密来启用这些要求。

# 1. 简介

　　JWT 是一个紧凑的要求表达格式，用于限制空间，例如 HTTP 授权头部和 URI 请求参数。JWTs 编码要求被作为一个 JSON 对象传输，作为 JWS 结构体的负载，或者作为 JWE 结构体的文本，通过数字签名或完整的信息授权码或加密来启用这些要求。

# 2. 术语

- JSON Web Token(JWT)
  - 一个代表被编码为一个 JWS 或 JWE 的一系列要求的 JSON 对象，通过数字签名或完整的信息授权码或加密来启用这些要求。

- JWT Claims Set
  - 一个包含被 JWT 传达包含一些列要求的 JSON 对象。

- Claim
  - 一段宣言一个主题的信息。一个要求表达为一个 name/value 值，由 Claim Name 和 Claim Value 组成。

- Claim Name
  - 要求的名字部分。通常是一个字符串。

- Claim Value
  - 要求的值部分。可以是任何 JSON 值。

- Nested JWT
  - 一个使用嵌套签名或加密的 JWT。在嵌套的 JWT 被用于 JWS 的负载或者 JWE 结构体的文本。

- Unsecured JWT
  - 一个没有被签名或加密的 JWT。

- Collision-Resistant Name
  - 一个规则命名空间中的名字，很大程度上不会有名字冲突。一个例子如下：域名，定义在 X.660 和 X.670 建议系列中的对象标识符(OIDs)，和 UUIDs。

- StringOrURI
  - 一个 JSON 字符串值，根据额外的需求，任意的字符串值可能被使用，任何包含 ":" 字母的值必须是 URI。

- NumericDate
  - 代表从  1970-01-01T00:00:00Z UTC 到指定 UTC 时间的，忽略闰秒。
