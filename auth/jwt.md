---
title: PHP JWT 详解
date: 2016-11-11 12:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Auth
---

`header.poyload.sign`

* 官方网站：https://jwt.io/

```bash
$ composer require firebase/php-jwt
```

<!--more-->

JWT 由三部分组成。

```bash
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

{
  "alg": "HS256",
  "typ": "JWT"
}

{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}

# 对上边两部分拼接成的字符串选择算法进行加密，生成 sign 签名
```

1. 用户输入 username、password 登录。

2. 服务器验证 username password

3. 获取用户信息，生成 token，返回 token

4. token 存入 cookie

认证过程

1. 请求头中加入 `Authorization: Bearer YOUR_JWT`

2. 服务器解密 token

3. 验证过期时间，验证权限

4. 返回结果
