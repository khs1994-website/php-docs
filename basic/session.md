---
title: PHP Session
date: 2016-10-12 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
---

`Session` 保存在服务端。保存在超全局变量 `$_SESSION`。

<!--more-->

# 设置 Session

在 `PHP` 文件最上方开启 `Session`

```php
session_start( [$options]);

$_SESSION(['username'])='username';
```

`PHPSESSIONID` 保存在服务端文件中，也将 id 保存在 `Cookie` 中。

## 通过 `Cookie` 设置 `Session` 生存期

```php
session_id( [$id]);

session_name( [$name]);

setcookie(session_name(),session_id(),time()+3600)
```

# 传递 Session id
