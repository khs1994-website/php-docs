---
title: PHP Cookie
date: 2016-10-11 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

`Cookie` 保存在客户端，分为 `内存 Cookie` 和 `硬盘 Cookie`。

<!--more-->

# 设置 Cookie

```php
setcookie($name [, $value, $expires, $path, $domain, $secure, $httponly])
```

`$path` 有效路径，默认是当前目录及其子目录

`$domain` 作用域，默认在本域下

`$secure` 只能通过 https 传输

`$httponly` 只使用 HTTP 访问 `Cookie`，如果设置为 `true`，客户端 `JS` 无法操作这个 `Cookie`

```php
setrawcookie($name [, $value, $expires, $path, $domain, $secure, $httponly])
```

不会对值进行 urlencode() 编码

# 读取 Cookie

存储在 `超全局变量` 中

`$_COOKIE`

# 更新 Cookie

`setcookie()` 设置新值

# 删除 Cookie

```php
setcookie($key,'',time()-1)
```

# header 操作 Cookie

```php
header("Set-Cookie:name=value[;expires=data]")
```

# 数组形式的 Cookie

```php
setcookie('userInfo[username]','username')
setcookie('userInfo[email]','khs1994@khs1994.com')
```
