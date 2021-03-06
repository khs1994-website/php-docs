---
title: PHP 面向对象
date: 2016-12-01T13:00:00.000Z
updated: null
comments: true
tags:
  - PHP
  - OOP
categories:
  - PHP
  - OOP
---

面向对象三大特性：`封装`、`继承`、`多态`。

官方文档：http://php.net/manual/zh/language.oop5.php

<!--more-->

要创建一个类的实例，必须使用 `new` 关键字。如果该类属于一个命名空间，则必须使用其完整名称。

你可以使用 `ClassName::class` 获取一个字符串，包含了类 `ClassName` 的完全限定名称。

# 常用关键字

当一个方法在类定义内部被调用时，有一个可用的伪变量 `$this`。`$this->属性` `$this->方法()` `$this::方法、常量、静态属性`（和 self 一致）

使用 `self::` 来访问方法、常量、静态属性。

使用 `static::` 后期 **静态绑定** ，`static::` 不再被解析为定义当前方法所在的类，而是在实际运行时计算的。

使用 `parent::` 来访问父类的方法和静态变量。

在类定义内部，可以用 `new self` 和 `new parent` 创建新对象。

# 常量、属性、方法

`属性` 中的变量可以初始化，但是初始化的值必须是常数，这里的常数是指 PHP 脚本在编译阶段时就可以得到其值，而不依赖于运行时的信息才能求值。

```php
/**
* 类常量可设置可见性
*
* @since 7.1
*/
class A
{
    public const VERSION = '18.03';
}
```

# 静态 `static` 关键字

* 静态方法

* 静态属性

# 访问控制

* `private`

* `protected`

* `public`

# 自动加载

```php
spl_autoload_register(function ($class_name) {
    require_once $class_name . '.php';
});
```

# 魔术方法

## 构造函数、析构函数

* `__construct()`

* `__destruct()`

析构函数即使在使用 `exit()` 终止脚本运行时也会被调用。在析构函数中调用 `exit()` 将会中止其余关闭操作的运行。

## 重载 动态地 `创建` 类属性和方法

* `__call()`

* `__callStatic()`

* `__get()`

* `__set()`

* `__isset()`

* `__unset()`

## 其他

* `__sleep()` 常用于提交未提交的数据，或类似的清理操作。同时，如果有一些很大的对象，但不需要全部保存，这个功能就很好用。`serialize()` 序列化对象时，首先调用该魔术方法。

* `__wakeup()` 经常用在反序列化操作中，例如重新建立数据库连接，或执行其它初始化操作。`unserialize()` 反序列对象时，首先被调用。

* `__toString()` 方法用于一个类被当成字符串时应怎样回应，例如 `echo $obj`。

* `__invoke()` 当尝试以调用函数的方式调用一个对象时，此方法会被调用。例如 `obj($arg)`。

* `__set_state()` 当调用 `var_export()` 导出类时，此静态方法会被调用。

* `__clone()` 对象被复制时被调用

* `__debugInfo()` 对对象使用 `var_dump()` 时，该方法被调用。例如 `var_dump(new MyClass(42));`


# 多态

# 对象继承 `extends`

一个类可以在声明中用 `extends` 关键字继承另一个类的方法和属性。

子类可以覆盖父类的属性或方法，当覆盖方法时，参数必须保持一致，否则 PHP 将发出 `E_STRICT` 级别的错误信息。但构造函数例外，构造函数可在被覆盖时使用不同的参数。

子类可以通过 `->` 调用父类的静态方法。

## `final` 禁止继承

如果父类中的方法被声明为 `final`，则子类无法覆盖该方法。如果一个类被声明为 `final`，则不能被继承。

用于 `类` 和 `方法` 前。

# 抽象类 `abstract`

抽象类中的抽象方法不能有具体实现。

抽象类中的普通方法有具体的实现。

抽象类不能被实例化。用于被其他类继承，子类必须定义抽象类中 **所有的** 抽象方法。

# 接口 `interface`

接口中的方法不能有具体实现。

接口中的方法必须公有。

## 实现接口 `implements`

实现接口的类必须实现接口中定义的 **所有的** 方法。

一个类可以实现多个接口，使用逗号分隔。

接口也可以继承接口 `extends`。接口可以继承多个接口。

接口常量不能被覆盖。

# 多继承 `trait`

## 一个类使用多个 `trait`

使用 `use`，并用逗号分隔。

```php
class MyClass {
  use Hello, World;

  public function ...
}
```

# 对象比较

# 遍历对象

# 类型约束

略

# 后期静态绑定 `static::`

`static::` 不再被解析为定义当前方法所在的类，而是在实际运行时计算的。也可以称之为 "静态绑定"，因为它可以用于（但不限于）静态方法的调用。

# 对象和引用

# 对象序列化

```php
// classa.inc:

class A {
    public $one = 1;

    public function show_one() {
          echo $this->one;
    }
}

// page1.php:

include("classa.inc");

$a = new A;
$s = serialize($a);
// 把变量$s保存起来以便文件page2.php能够读到
file_put_contents('store', $s);

// page2.php:

// 要正确了解序列化，必须包含下面一个文件
include("classa.inc");

$s = file_get_contents('store');
$a = unserialize($s);

// 现在可以使用对象$a里面的函数 show_one()
$a->show_one();
```

# 对象复制 `__clone() 魔术方法`

```php
class AB{
  public $a = 1;
  public $b = 2;

  public function __clone(){
    echo "对象被克隆了";
    $this->a=2;
  }
}

$ab = new AB();

$abc = clone $ab;
```

# PHP 7 新特性

## 匿名类

```php
$a = (new class {
    public function log($msg)
    {
        echo $msg;
    }
});

$a->log('hello');
```
