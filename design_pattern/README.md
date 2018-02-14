---
title: PHP 设计模式
date: 2018-01-31 13:00:00
updated:
comments: true
tags:
- PHP
- Design_Pattern
categories:
- PHP
- Design_Pattern
---

工厂模式、单例模式、注册树模式...

<!--more-->

# 工厂模式

工厂方法或者类生成对象，而不是直接 `new` 对象。

```php
class F
{
    static function createDocker($arg){
        // return new Docker($arg);

        // 单例模式

        $docker = B::getDocker($arg);

        // 注册树模式
        // 将对象注册到 docker

        R::set('docker',$docker);

        // 返回对象

        return $docker;
    }
}

// $docker = A::createDocker($arg);

$docker = R::get('docker');

$docker->container->list();
```

# 单例模式

某个类的对象仅允许创建一次。

```php
Class D
{
    private $docker;

    // 构造函数为私有，外部不能直接 new

    private function __construct($arg){
        echo $arg;
    }

    public static function getDocker($arg){
        if (! self::$docker){
          // 静态函数中 new 对象
          self::$docker=new self();
        }

        return self::$docker;
    }
}

$docker = B::getDocker($arg);

$docker->container->list();
```

# 注册树模式

全局共享和交换对象。

```php
class R
{
    private static $obj;

    public static function set($name, $obj){
        self::obj[$name]=$obj;
    }

    public static function unset(){
        unset(self::$obj);
    }

    public static function get($name){
        return self::$obj[$name];
    }
}
```
