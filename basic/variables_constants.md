---
title: PHP 变量与常量
date: 2016-10-21 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

本文介绍了 PHP 变量与常量。

官方文档：http://php.net/manual/zh/language.variables.php

官方文档：http://php.net/manual/zh/language.constants.php

<!--more-->

# `global` 关键字

# `$GLOBALS` 数组

# 静态变量

函数中的静态变量，函数执行完毕后，其值被保留。

# 可变变量

```php
$a='hello';

$$a='world'; // 即 $hello='world';
```

# 超全局变量

`$GLOBALS`

`$_SERVER` 服务器和执行环境信息

`$_POST`

`$_GET`

`$_REQUEST`

`$_FILES`

`$_SESSION`

`$_COOKIE`

`$_ENV` 环境变量

# 常量

常量的范围是全局的。

常量一旦定义就不能被重新定义或者取消定义。

常量的值只能是标量。

## 定义常量

```php
define('FOO', 'bar');
```

```php
const FOO = 'bar';
```

const 不能用在函数内、循环内、if 语句之内。

## 获取常量

使用 `constant()` 来获取常量值。

使用 `get_define_constants()` 获得所有已定义的常量。

## 魔术常量

`__LINE__` `__FILE__` 等
