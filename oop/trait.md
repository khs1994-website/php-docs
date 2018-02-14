---
title: PHP 面向对象 trait
date: 2016-12-06T13:00:00.000Z
updated: null
comments: true
tags:
  - PHP
  - OOP
categories:
  - PHP
  - OOP
---

通过 `trait` 可以实现多继承。

<!-- more -->

```php
trait A
{
    public function fun1()
    {
        echo __FUNCTION__;
    }
}

trait B
{
    public function fun2()
    {
        echo __FUNCTION__;
    }
}

// trait 中可以使用其他 trait

trait D{
  use A, B;
}

class C
{
    // 可以使用 use 列出多个 trait
    use A,B;
}

$c=new C();

$c->fun1();
```
