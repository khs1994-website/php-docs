---
title: PHP 面向对象
date: 2016-10-18T13:00:00.000Z
updated: null
comments: true
tags:
  - PHP
categories:
  - PHP
  - Basic
---

本文记录了 PHP 面向对象的知识。

<!--more-->

# 属性、方法、类常量

# 静态 `static`

* 静态方法

* 静态属性

# 访问控制

* private

* protected

* public

# 魔术方法

# 构造函数、析构函数

* `__construct()`

* `__destruct()`

# 重载

> `overloading` 动态地「创建」类属性和方法，通过魔术方法实现。

当调用当前环境下未定义或不可见的类属性或方法时，重载方法会被调用。

## 属性重载

* `__set(string $name,mixed $value)` 给不可访问属性赋值时

* `__get(string $name)` 读取不可访问属性

* `__isset(string $name)` 对不可访问属性调用 `isset()` `empty()`

* `__unset(string $name)` 对不可访问属性调用 `unset()`

## 方法重载

* `__call(string $name,array $arguments)` 在对象中调用不可访问的方法

* `__callStatic(string $name,array $arguments)`

# 对象继承

# `final` 禁止继承

# 抽象类 `abstract`

抽象类不能被实例化。用于被其他类继承，子类必须定义抽象类中所有的抽象方法。

# 接口 `interface`

接口中的方法必须公有。

## 实现接口

`implements`

实现接口的类必须实现接口中定义的 **所有** 方法。

一个类可以实现多个接口，使用逗号分隔。

接口也可以继承。

接口常量不能被覆盖。

# 多继承 `trait`

## 一个类使用多个 `trait`

使用 `use`，并用逗号分隔。

# 匿名类

# 多态
