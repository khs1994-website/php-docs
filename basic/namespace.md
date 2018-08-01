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

* http://php.net/manual/zh/language.namespaces.php

<!--more-->

# 一般规则

* 文件路径 + 类名（文件名与类名保持一致）

```php
namespace A\B;  // 定义命名空间，在所有代码之前声明，除了 declare()

/**
* use 关键字导入命名空间
* namespace 与 use 之间空一行
*/

/**
* @since 7.0 分组命名空间，7.2 允许尾部逗号
*/

use Foo\Bar\{
    Foo,
    Bar,
    Baz,
};

use Error; // 全局空间

use Foo\Bar as BarBase; // 别名

use function C\D\functionName as func;

use const C\D\CONSTANT;

function a()
{

}

class A
{

}

// PHP 支持两种抽象的访问当前命名空间内部元素的方法，__NAMESPACE__ 魔术常量和 namespace 关键字。

namespace\a();

$my_class = __NAMESPACE__ . '\\A';

$obj = new $my_class();

// 在命名空间内，用一个变量来动态调用类，必须加上命名空间。

// $my_class_error = 'A';

// $obj = new $my_class_error();

$f = \fopen(); // 调用全局的函数
```
