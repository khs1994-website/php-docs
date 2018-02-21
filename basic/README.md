---
title: khs1994.com PHP 开发规范
date: 2016-10-20 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

`khs1994.com` PHP 开发规范。

<!--more-->

# 编码规范

关键字必须小写 `true`, `false`, `null`。

## 类

类的 `属性` 和 `方法` 必须添加访问修饰符 `private`、`protected` 以及 `public`。

`abstract` 以及 `final` 必须声明在访问修饰符之前。

`static` 必须声明在访问修饰符之后。

### 类名

大驼峰 `StudlyCaps`

### 方法

小驼峰 `cameCase`

各个方法之间有一个空行。

### 属性

`一定不可` 使用关键字 `var` 声明一个属性

## 函数名

小写 + 下划线 `json_to_array`

各个函数之间有一个空行。

如果 `return` 语句之前只有一行 PHP 代码，`return` 语句之前不需要空行。

如果 `return` 语句之前有至少有两行 PHP 代码，`return` 语句之前加一个空行。

## 变量

小驼峰 `cameCase`

## 常量

大写 + 下划线 `APP_KEY`

# 依赖管理

使用 `composer` 管理依赖。

# More Information

* https://github.com/PizzaLiu/PHP-FIG/blob/master/PSR-2-coding-style-guide-cn.md
