---
title: PHP 多态
date: 2016-12-05T13:00:00.000Z
updated: null
comments: true
tags:
  - PHP
  - OOP
categories:
  - PHP
  - OOP
---

使用接口和类型提示实现多态

<!--more-->

* 根据使用类的上下文来重新定义或改变类的性质和行为

* 不同的对象，执行相同的方法，而又取得不同的结果

```php
interface Animal
{
  public function eat();
}

class Cat implements Animal
{
  public function eat(){
    echo "cat eat";
  }
}

class Dog implements Animal
{
  public function eat(){
    echo "dog eat";
  }
}

class Demo
{
  public function eat(Animal $animal)
  {
    $animal->eat();
  }
}

$demo=new Demo;

$demo->eat(new Dog());

$demo->eat(new Cat());
```
