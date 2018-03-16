---
title: PHP 命名空间
date: 2016-10-22 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

`PHP` 命名空间解决了可能发生的冲突的问题。

<!--more-->

```php
namespace A\B;  // 定义命名空间，在所有代码之前声明，除了 declare()

/**
* use 关键字导入命名空间
* namespace 与 use 之间空一行
*/

/**
* @since 7.2 分组命名空间，允许尾部逗号
*/

use Foo\Bar\{
    Foo,
    Bar,
    Baz,
};

// 全局空间

use \Error;

// 别名

use Foo\Bar as BarBase
```
