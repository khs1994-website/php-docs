---
title: PHP 数据类型
date: 2016-10-5 12:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
- Types
---

PHP 支持三大类 8 种数据类型。

官方文档：http://php.net/manual/zh/language.types.php

<!--more-->

# 标量（4）

* 布尔 `boolean`

* 整型 `integer`

* 浮点型 `float` or `double`

* 字符型 `string`

# 复合类型（2）

* 数组 `array`

* 对象 `object`

# 特殊类型 （2）

* 资源 `resource`

* `NULL`

# 其他类型

* 回调类型 `callback`

* 伪变量 `...$var`

* 函数返回值为空 `void`

# 相关函数

* `var_dump()` 查看值和类型

* `gettype()` 获得类型

* `is_type` 函数，例如 `is_int()` `is_string()` 返回布尔类型

* 类型转换，强制转换或 `settype()` 函数

* 转化 `(int) false` 将布尔类型转化为整数

# More Information

* PHP 类型比较表: http://php.net/manual/zh/types.comparisons.php
