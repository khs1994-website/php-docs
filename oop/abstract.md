---
title: PHP 面向对象 抽象类
date: 2016-12-02T13:00:00.000Z
updated: null
comments: true
tags:
  - PHP
  - OOP
categories:
  - PHP
  - OOP
---

使用 `abstract` 关键字申明抽象类和抽象方法。抽象类不能被实例化，只能被其他类继承。

<!--more-->

```php
abstract class A
{
    // 抽象方法没有函数体，即具体实现

    abstract protected function fun1();

    abstract protected function fun2($num);

    // 普通方法，即非抽象方法

    public function fun3()
    {
        echo __FUNCTION__;
    }
}

class B extends A
{
    // 子类必须定义抽象类中的所有抽象方法

    public function fun1()
    {
        echo __FUNCTION__;
    }

    // 子类方法的访问控制，必须和抽象类中方法的访问控制一致，或更为宽松

    // 参数必须一致，但子类可以定义父类方法中不存在的可选参数

    public function fun2($num, $num2='0')
    {
        echo $num;
    }
}

// 抽象类不能被实例化

$b=new B();

$b->fun2(1);
```
