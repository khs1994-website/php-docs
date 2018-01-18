---
title: PHP 面向对象 重载
date: 2016-12-04T13:00:00.000Z
updated: null
comments: true
tags:
  - PHP
  - OOP
categories:
  - PHP
  - OOP
---

> `overloading` 动态地「创建」类属性和方法，通过魔术方法实现。

<!--more-->

当调用当前环境下未定义或不可见的类属性或方法时，重载方法会被调用。

## 属性重载

* `__set(string $name,mixed $value)` 给不可访问属性赋值时

* `__get(string $name)` 读取不可访问属性

* `__isset(string $name)` 对不可访问属性调用 `isset()` `empty()`

* `__unset(string $name)` 对不可访问属性调用 `unset()`

## 方法重载

* `__call(string $name,array $arguments)` 在对象中调用不可访问的方法

* `__callStatic(string $name,array $arguments)`
