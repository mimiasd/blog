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

# 3. 概述

　　JWTs 代表被编码为 JWS 或 JWE 结构体的由一系列声明组成的 JSON 对象。这个 JSON 对象是 JWT 的声明集。JSON 对象由一系列零或更多的 name/value 对(或成员)，其中 name 是字符串，value 是任意 JSON 对象值。这些成员是被 JWT 表达的声明。

　　JWT 声明集中的成员值指声明的名字。对应值指声明值。

　　JOSE(Javascript Object Signing and Encryption) 的内容描述了 JWT 声明集的加密操作。如果 JOSE Header 是对一个 JWS，那么 JWT 的声明集被数字签名或使用信息识别码，作为 JWS 的负载。如果 JOSE Header 是对一个 JWE，那么声明集将被加密，作为 JWE 的加密文本。一个 JWT 可能被附在另一个 JWE 或 JWS 结构体上来创建一个嵌套的 JWT，来使嵌套的签名和加密执行。

　　一个 JWT 被表述为一系列 URL 安全的由 "." 隔开的字符集。每个部分包含一个 Base64URL 编码的值。JWT 部分的数量取决于使用 JWS 序列化还是 JWE 序列化。

## 3.1 JWT 的例子

　　下面的 JOSE Header 声明编码对象是一个 JWT，这个 JWT 是一个 JWS，使用 HMaC SHA-256 算法的信息识别码：

```
{"typ":"JWT",
"alg":"HS256"}
```

　　为了移除上述表述的潜在歧义性，由下面的确切 UTF-8 八位字节序列表示。(注意歧义可能在不同平台表述换行符，行首或行尾不同的空格)：

```
 [123, 34, 116, 121, 112, 34, 58, 34, 74, 87, 84, 34, 44, 13, 10, 32, 34, 97, 108, 103, 34, 58, 34, 72, 83, 50, 53, 54, 34, 125]
```

　　Base64Url 编码上面的 UTF-8 八位字节序列表示，产生下面的值：

```
eyJ0eXAiOiJKV1QiLA0KICJhbGciOiJIUzI1NiJ9
```

　　下面是一个 JWT 声明集：

```
{"iss":"joe",
 "exp":1300819380,
 "http://example.com/is_root":true}
```

　　下面是以上的 JWT 声明集 UTF-8 表示：

```
[123, 34, 105, 115, 115, 34, 58, 34, 106, 111, 101, 34, 44, 13, 10,
32, 34, 101, 120, 112, 34, 58, 49, 51, 48, 48, 56, 49, 57, 51, 56,
48, 44, 13, 10, 32, 34, 104, 116, 116, 112, 58, 47, 47, 101, 120, 97,
109, 112, 108, 101, 46, 99, 111, 109, 47, 105, 115, 95, 114, 111,
111, 116, 34, 58, 116, 114, 117, 101, 125]
```

　　使用 Base64Url 编码为：

```
eyJpc3MiOiJqb2UiLA0KICJleHAiOjEzMDA4MTkzODAsDQogImh0dHA6Ly
9leGFtcGxlLmNvbS9pc19yb290Ijp0cnVlfQ
```

　　计算编码后的 JOSE Header 的信息识别码，并且通过 HMAC SHA-256 算法编码 JWS 负载，然后使用 Base64Url 编码 HMAC 的值，来产生 JWS 签名：

```
dBjftJeZ4CVP-mB92K27uhbUJU1p1r_wW1gFWFOEjXk
```

　　把这编码的三部分用 "." 连接在一起组成完整的 JWT：

```
eyJ0eXAiOiJKV1QiLA0KICJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJqb2UiLA0KICJleHAiOjEzMDA4MTkzODAsDQogImh0dHA6Ly9leGFtcGxlLmNvbS9pc19yb290Ijp0cnVlfQ.dBjftJeZ4CVP-mB92K27uhbUJU1p1r_wW1gFWFOEjXk
```

# 4. JWT 声明

　　JWT 声明集是一个 JSON 对象，成员是 JWT 传达的声明。声明名字必须是唯一的；JWT 解析器必须拒绝有重复名字的 JWTs，或者使用一个 JSON 解析器返回词汇上最后一个成员名字。

　　JWT 的声明集必须包含有效的内容。

　　这有三种 JWT 声明名字：注册的声明名，公开的声明名，私有的声明名。

## 4.1 注册的声明名

　　下面的声明名是注册在 IANA 上的声明名。下面没有一个声明是强制使用的或在所有情况下都是用，但它们提供了一个声明集的起点，互操作的声明。使用 JWTs 的应用需要定义他们使用的哪些指定的声明，必须的或可选的。所有的名字是简短的，因为 JWTs 的核心目标是做到表达紧凑。

### 4.1.1 "iss"(Issuer) Claim

　　"iss" 声明指示发放该 JWT 的当事人。处理该声明的过程通常是应用指定的。"iss" 值是一个大小写敏感包含一个 StringOrURI 值的字符串。该声明的使用是可选的。

### 4.1.2 "sub"(Subject) Claim

　　"sub" 声明指示发放该 JWT 的主题。JWT 中的该声明是关于主题的陈述。主题的值必须是发布者文本内部唯一的或全局唯一的。处理该声明的过程通常是应用指定的。"sub" 值是一个大小写敏感包含一个 StringOrURI 值的字符串。该声明的使用是可选的。

### 4.1.3 "aud"(Audience) Claim

　　"aud" 声明指示该 JWT 的接收人。每一个要执行 JWT 的当事人必须在接收人声明中标志自己。当该声明被使用时，如果当事人没有在 "aud" 中标志自己，那么该 JWT 必须被拒绝。在通常情况下，"aud" 声明是大小写敏感的字符串数组，包含一个 StringOrURI 值。处理该声明的过程通常是应用指定的。该声明的使用是可选的。

### 4.1.4 "exp"(Expiration Time) Claim

　　"exp" 声明指示该 JWT 的到期时间，在这之后该 JWT 必须不能被接收。该声明要求当前时间必须在到期时间范围以内，实现者可能提供一点回旋的余地，通常不超过几分钟，来算上时间倾斜。它的值必须包含一个数字化的时间。该声明的使用是可选的。

### 4.1.5 "nbf"(Not Before) Claim

　　"nbf" 声明指示该 JWT 在该时间以前不能被接受。"nbf" 声明要求当前时间必须在该时间之后或等于该时间。实现者可能提供一点回旋的余地，通常不超过几分钟，来算上时间倾斜。它的值必须包含一个数字化的时间。该声明的使用是可选的。

### 4.1.6 "iat"(Issued At) Claim

　　"iat" 声明指示该 JWT 被发放的时间。该声明可以用来决定 JWT 的寿命。它的值必须包含一个数字化的时间。该声明的使用是可选的。

### 4.1.7 "jti"(JWT ID) Claim

　　"jti" 声明指示该 JWT 的唯一标识符。该标识符必须保证只有微小的可能性会重复。如果应用使用了多个发布者，那么不同发布者的冲突可能性必须被制止。"jti" 声明用来防止 JWT 被重新使用。"jti" 的值是一个大小写敏感的字符串。该声明的使用是可选的。

## 4.2 公共的声明名

　　声明名可以根据这些使用 JWTs 的需要。然而，为了避免冲突，任何新的声明名应该在 IANA 中注册，或成为一个公共名：一个包含避免冲突的名字值。在每个情况下，名字和值的定义者都需要预先避免冲突，保证命名空间在他们的掌控之下。

## 4.3 私人的声明名

　　一个 JWT 的生成和使用者可能同意使用的声明名是私有声明名：没有被注册的声明名或者公共的声明名。不像公共的声明名，私有声明名受制于冲突，使用需谨慎。

# 5. JOSE Header

　　对于一个 JWT 对象，JOSE Header 对象描述的作用于 JWT 和可选的该 JWT 性质的加密操作方法。取决于该 JWT 是一个 JWS 还是 JWE，使用对应的 JSOE Header 规则。

　　下面的参数在两种情况都可以使用。

## 5.1 "typ"(Type) 头部参数

　　"typ" 头部参数被 JWS 和 JWE 定义来声明完整 JWT 的应用媒体类型。这个可以被 JWT 应用是用来使那些非 JWTs 可以包含一个 JWT 结构体。应用可以使用该值来区分不同的对象类型。当已知是一个 JWT 对象时，没有必要使用该值。该值被 JWT 实现忽略。任何对该参数的处理都在 JWT 的应用中。如果提供了，那么推荐该值为 "JWT" 来标志该对象是一个 JWT 类型。因为媒体类型不是大小写敏感的，推荐使用 "JWT" 的大写形式。该头部参数的使用是可选的。

## 5.2 "cty"(Content Type) 头部参数

　　"cty" 头部参数被 JWS 和 JWE 定义来传达 JWT 结构化的信息。

　　在通常没有嵌套签名或加密的情况下，使用该头部参数是不推荐的。在有嵌套的情况下，该值必须存在，且为 "JWT"。

## 5.3 复制声明作为头部参数

　　在一些使用加密的 JWTs 应用下，有一个关于一些未加密的声明是有用的。例如，应用执行规则来决定是否和怎么处理 JWT，在它被解密之前。

# 6. 未结构化的 JWTs

　　JWTs 可能不适用包含数据结构的签名。

# 7. 创建和验证 JWTs

## 7.1 创建一个 JWT

　　为了创建一个 JWT，将有接下来的步骤。步骤的顺序并不重要，因为步骤间的输入和输出是没有依赖的。

1. 创建一个包含需要的 JWT 声明集。注意：空格是明确允许的在这个表述中，在编码之前没有规范。

2. 让该声明集信息以八进制的 UTF-8 表述。

3. 创建一个包含需要的头部参数集的 JOSE Header。JWT 必须根据 JWS 或 JWE 说明书。注意：空格是明确允许的在这个表述中，在编码之前没有规范。

4. 下面有两种情况，取决于 JWT 是 JWS 或 JWE：

- 如果 JWT 是一个 JWS，那么使用该信息作为 JWS 的负载。

- 如果 JWT 是一个 JWE，那么使用该信息作为 JWE 的加密文本。

5. 如果一个嵌套的签名或加密操作被执行，让信息成为 JWS 或 JWE，回到第三步，使 "cty" 的值为 "JWT" 在新创建的 JOSE Header 步骤中。

6. 否则，使 JWT 的结果成为 JWS 或者 JWE。

## 7.2 验证一个 JWT

　　为了验证一个 JWT，将有接下来的步骤。步骤的顺序并不重要，因为步骤间的输入和输出是没有依赖的。如果有任何一步失败了，那么 JWT 必须被拒绝 - 即被应用作为一个无效的输入。

1. 验证 JWT 至少含有一个 "."。

2. 获得 JWT 中第一个 "." 之前的 JOSE Header 部分。

3. 用 Base64URL 解码编码的 JOSE Header，根据没有换行符，空格号，或其他使用的额外字符的限制。

4. 验证得到的 UTF-8 编码的描述是一个完整的有效 JSON 对象。让 JOSE Header 作为这个 JSON 对象。

5. 验证 JOSE Header 的结果只包括参数和值，它们的语法和语义都是能被理解和支持的，当不被理解的时候将被忽略。

6. 决定 JWT 是一个 JWS 或 JWE。

7. 以下有两个选择，取决于 JWT 是 JWS 或 JWE：

- 如果 JWT 是一个 JWS，则按 JWS 的步骤验证。并使用 Base64URL 来解码 JWS 的负载。

- 如果 JWT 是一个 JWE，则安 JWE 的步骤验证。并使用结果中的明文。

8. 如果 JOSE Header 中包含一个 "cty" 值为 "JWT"，那么这是一个嵌套的 JWT 对象。这时，回到步骤 1。

9. 否则，使用 Base64URL 解码该信息，根据没有换行符，空格号，或其他使用的额外字符的限制。

10. 验证最终的 UTF-8 字符序列是一个完整的 JSON 对象。让 JWT 声明集成为该 JSON 对象。

　　最后，注意是应用决定使用那个算法被使用于一个给定文本。即使 JWT 被成功验证，但如果算法不被应用接收，也会被拒绝。

## 7.3 字符串比较规则

　　处理一个 JWT 必将需要比较已知的字符串和 JSON 对象中的值。例如，为了检查使用的哪种算法，编码为 Unicode 字符串的 "alg" 将被与 JOSE Header 中的参数名进行比较。

　　
