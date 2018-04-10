---
title: PHP 面向对象 接口
date: 2016-12-03T13:00:00.000Z
updated: null
comments: true
tags:
  - PHP
  - OOP
categories:
  - PHP
  - OOP
---

使用接口 `interface`，可以指定某个类必须实现哪些方法，但不需要（**也不能**）定义这些方法的具体内容。

要实现一个接口，使用 `implements` 操作符。

接口中定义的所有方法都必须是公有，这是接口的特性。

<!--more-->

接口可以继承另一个接口，接口可以一次继承多个接口。

```php
interface D
{
    public function fun4();
}

interface A
{
    // 接口常量不能被子类或子接口覆盖

    const VERSION='0.0.1';

    // 接口中的方法都没有具体实现

    public function fun1();

    public function fun2($num);
}

interface C extends D{
  public function fun3();
}

// 一个类可以实现多个接口

class B implements A, D
{

    // 子类中必须实现接口中定义的所有方法

    public function fun1()
    {
        echo __FUNCTION__;
    }

    // 参数要求与抽象类一致

    public function fun2($num, $num2=0)
    {
        echo $num;
    }

    public function fun3()
    {
        echo __FUNCTION__;
    }

    public function fun4()
    {
        echo __FUNCTION__;
    }
}

// 接口不能被实例化

$b=new B();

$b->fun1();
```
