---
title: "Jws"
date: 2018-03-11T13:40:03+08:00
lastmod: 2018-03-11T13:40:03+08:00
draft: false
keywords: [jws]
description: ""
tags: [jws]
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

> [JWS RFC](https://tools.ietf.org/html/rfc7515)

# JWS

　　JWS 表示被数字签名或信息识别码保证的使用基于 JSON 数据结构的内容。该说明书用的加密算法定义在 JWA(JSON Web Algorithms) 中。相对应的加密功能定义在 "JWE" 中。

# 1. 简介

　　JWS 表示被数字签名或信息识别码保证的使用基于 JSON 数据结构的内容。JWS 的加密机制提供了对任意八位元组的完整性保护。有两个对应的 JWSs 序列化方法。JWS Compact Serialization 是一个紧凑的，URL 安全的表示，对应于空格严格的环境，例如 HTTP 授权头和 URI 请求参数。JWS JSON Serialization 表示把 JWSs 作为一个 JSON 对象，使多个签名或 MACS 作用于同样的内容。它们同时使用同样的加密底层。

　　该说明书用的加密算法定义在 JWA(JSON Web Algorithms) 中。相对应的加密功能定义在 "JWE" 中。

# 2. 术语

　　下面是该说明书中的文档：

- JSON Web Signature(JWS)
  - 一个表示被数字签名或信息识别码处理的消息。

- JOSE Header
  - 包含加密操作和使用参数的 JSON 对象。JOSE(JSON Object Signing and Encryption) Header 由一系列头部参数组成。

- JWS Payload
  - 被保证的八位元组序列 - 即消息。负载可以包含一个任意的八位元组。

- JWS Signature
  - 通过数字签名或 信息识别码来保护 JWS 头部和负载。

- Header Parameter
  - 一个 名字/ 值 对，是 JOSE Header 的成员。

- JWS Protected Header
  - 包含头部参数的被 JWS 数字签名或信息识别码操作进行完整性保护的 JSON 对象。对于 JWS Compact Serialization，这包括了整个的 JOSE Header。对于 JWS JSON Serialization，这是一个 JOSE Header 的一部分。

- JWS Unprotected Header
  - 没有进行完整性保护的头部。当使用 JWS JSON Serialization 时，这可以被提出。

- Base64Url Encoding
  - URL 和 filename 安全的 Base64 编码字符集。

- JWS Signing Input
  - 数字签名或信息识别码计算的输出。它的内容是：ASCII(BASE64URL(UTF8(JWS Protected Header)) || '.' || BASE64URL(JWS Payload))。

- JWS Compact Serialization
  - JWS 一个紧凑的，URL 安全的字符串表示。

- JWS JSON Serialization
  - JWS 的 JSON 对象表示。和上面的不同，JSON 对象表示使用了多个数字签名或信息识别码作用于同样的内容。这对间接性和 URL 安全性都没有优化。

- Unsecured JWS
  - 没有提供完整性保护的 JWS。使用 "alg" 参数设为 "none"。

- Collision-Resistant Name
  - 一个高度避免冲突的命名空间。

- StringOrURI
  - 一个 JSON 字符串值，包括需要的任意字符串值都可能被使用，包括 ":"。

# 3. JWS 概述

　　一个 JWS 有以下逻辑值：

- JOSE Header
- JWS Payload
- JWS Signature

　　对于一个 JWS，JOSE Header 是下面这些成员的组合：

- JWS Protected Header
- JWS Unprotected Header

　　两个序列化方法都使用 base64URL 编码 JWS Protected Header，JWS Payload 和 JWS Signature，因为 JSON 缺少一个直接表达任意八位元组的方法。

## 3.1 JWS Compact Serialization 概述

　　在 JWS Compact Serialization 中，没有使用 JWS Unprotected Header。在这个情况下，JOSE Header 和 JWS Protected Header 是一样的。

　　在 JWS Compact Serialization 中，一个 JWS 由以下串联表示：

```
BASE64URL(UTF8(JWS Protected Header)) || '.' ||
BASE64URL(JWS Payload) || '.' ||
BASE64URL(JWS Signature)
```

## 3.2 JWS JSON Serialization 概述

　　在 JWS JSON Serialization 中，一个或同时 JWS Protected Header和 JWS UNProtected Header 必须被使用。在这种情况下，JOSE Header 是两者的联合。

　　在一个 JWS JSON Serialization 中，一个 JWS 表示包含以下一些或全部的四个成员：

- "protected"，参数为：BASE64URL(UTF8(JWS Protected Header))
- "header"，参数为： JWS Unprotected Header
- "payload"，参数为：BASE64URL(JWS Payload)
- "signature"，参数为：BASE64URL(JWS Signature)

　　三个基于 Base64Url 编码的结果字符串和 JWS Unprotected Header 被表达为一个 JSON 对象的成员。

## 3.3 JWS 的例子

　　该节提供一个 JWS 的例子。

　　接下来的 JWS Protected Header 声明为一个 JWT，JWS 的负载使用的是 HMAC SHA-256 算法保护：

```
{"typ":"JWT",
 "alg":"HS256"}
```

　　编码该受保护的头部使用 BASE64URL(UTF8(JWS Protected Header)) 方法，得到如下值：

```
eyJ0eXAiOiJKV1QiLA0KICJhbGciOiJIUzI1NiJ9

```

　　下面的表述的 UTF-8 形式作为 JWS 的负载(负载可以为任意的内容，不需要只被描述为一个 JSON 对象)：

```
{"iss":"joe",
 "exp":1300819380,
 "http://example.com/is_root":true}
```

　　使用 Base64URL(JWS Payload) 编码 JWS Payload，得到如下值：

```
eyJpc3MiOiJqb2UiLA0KICJleHAiOjEzMDA4MTkzODAsDQogImh0dHA6Ly9leGFtcGxlLmNvbS9pc19yb290Ijp0cnVlfQ
```

　　计算 JWS Signing 输入 ASCII(BASE64URL(UTF8(JWS Protected Header)) || '.' || BASE64URL(JWS Payload)) 的 HMAC，得到 BASE64URL(JWS Signature) 的值如下：

```
dBjftJeZ4CVP-mB92K27uhbUJU1p1r_wW1gFWFOEjXk
```

　　把这些值按 Header.Payload.Signature 的顺序连接起来，组成完整的 JWS 表述，使用 JWS Compact Serialization：

```
eyJ0eXAiOiJKV1QiLA0KICJhbGciOiJIUzI1NiJ9
.
eyJpc3MiOiJqb2UiLA0KICJleHAiOjEzMDA4MTkzODAsDQogImh0dHA6Ly9leGFtcGxlLmNvbS9pc19yb290Ijp0cnVlfQ
.
dBjftJeZ4CVP-mB92K27uhbUJU1p1r_wW1gFWFOEjXk
```
