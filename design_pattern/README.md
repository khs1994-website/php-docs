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
class Factory
{
    public static function createFactory($arg){
        // return new Docker($arg);

        // 单例模式

        $docker = Instance::getInstance($arg);

        // 注册树模式

        Register::set('docker',$docker);

        // 返回对象

        // return $docker;
    }
}

$docker = Factory::createFactory($arg);

$docker = Register::get('docker');

$docker->container->list();
```

# 单例模式

某个类的对象仅允许创建一次。

三私一公。

```php
Class Instance
{
    private $instance;

    // 构造函数为私有，外部不能直接 new

    private function __construct($arg){
        echo $arg;
    }

    // 禁止对象被克隆
    private function __clone(){

    }

    public static function getInstance($arg){
        if (!(self::$instance instanceof self)){
          // 静态函数中 new 对象
          self::$instance=new self();
        }

        return self::$instance;
    }
}

$docker = Instance::getInstance($arg);

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

# 观察者模式

将 观察者实例 注入到 主题 中

```php
// 主题
class Subject
{
  public $observers;

  public function register(ObServer $observer){
    $this->observers[]=$arg;
  }

  public function notify(){
    foreach ($this->observers as $key) {
      $key->watch();
    }
  }
}

// 观察者接口
interface Observer
{
  public function watch();
}

// 观察者
class Cat implements Observer
{
  public function watch(){
    echo "cat watch";
  }
}

$subject = new Subject();

$subject->register(new Cat());

$subject->notify();
```
