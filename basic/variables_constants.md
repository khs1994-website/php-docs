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

# 静态变量

静态变量仅在局部函数域中存在，但当程序执行离开此作用域时，其值并不丢失。

```php
function test()
{
    static $a = 0;
    echo $a;
    $a++;
}
```

# `global` 关键字

# `$GLOBALS` 数组

# 可变变量

```php
$a='hello';

$$a='world'; // 即 $hello='world';
```

# 超全局变量

* `$GLOBALS`

* `$_SERVER` 服务器和执行环境信息

* `$_POST` `$_GET`

* `$_REQUEST`

* `$_FILES`

* `$_SESSION` `$_COOKIE`

* `$_ENV` 环境变量

# 其他预定义变量

* `$http_response_header` HTTP 相应头

* `$argc` 传递给脚本的参数 **数目**

* `$argv` 传递给脚本的参数数组

# 常量

常量的范围是全局的，常量一旦定义就不能被重新定义或者取消定义。

常量的值只能是标量。

## 定义常量

```php
define('FOO', 'bar');

const FOO = 'bar';
```

`const` 不能用在函数、循环、if 语句之内。

## 获取常量

* `constant()` 获取常量值。

* `get_define_constants()` 获得所有已定义的常量。

## 魔术常量

* http://php.net/manual/zh/reserved.constants.php

`__LINE__`

`__FILE__` `__DIR__`
