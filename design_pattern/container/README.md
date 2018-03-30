---
title: PHP 服务容器（资料聚合）
date: 2018-03-23 13:00:00
updated:
comments: true
tags:
- PHP
- Design_Pattern
categories:
- PHP
- Design_Pattern
---

* IOC `控制反转`

* DI `依赖注入`

<!--more-->

```php
// 实现容器
// DB 类 Session 类 FileSystem 类 省略

class Container{
    public $bindings;
    /**
    * 将 闭包 与 别名 对应起来，和注册树模式差不多
    */
    public function bind($abstract,$concrete){
        $this->bindings[$abstract]=$concrete;
    }

    // 调用
    public function make($abstract,$parameters=[]){
        return call_user_func_array($this->bindings[$abstract],$parameters);
        // 参数传入 回调函数，完成类实例化（返回的是一个对象，即类的实例）
    }
}

// 服务注册

$container=new Container();

$container->bind('db',function($arg1,$arg2){
    // 回调函数中实例化类，即返回对象
    return new DB($arg1,$arg2);
});

$container->bind('session',function($arg1,$arg2){
    return new Session($arg1,$arg2);
});

$container->bind('fs',function($arg1,$arg2){
    return new FileSystem($arg1,$arg2);
});

// 容器依赖

class Writer{
    protected $_db;
    protected $_filesystem;
    protected $_session;
    protected $container;
    public function Writer(Container $container){
        // 将对象赋值给对象属性
        $this->_db=$container->make('db',[1,2]);
        $this->_filesystem=$container->make('session',[3,4]);
        $this->_session=$container->make('fs',[5,6]);
    }
}

$writer=new Writer($container);
```

# 依赖注入

只要不是由内部生产（比如初始化、构造函数中通过工厂方法、自行手动 new 的），而是由外部以参数或其他形式注入的，都属于 `依赖注入（DI）`。

# 反转

所谓的反转，主要指由 主动依赖 到 被动依赖 。

```php
//主动依赖
function __construct() {
        $this->user = new UserModel();
}

//被动依赖
function __construct(UserModel $user) {
        $this->user = $user;
}
```

# Links

* https://www.cnblogs.com/sweng/p/6430374.html

* https://laravel-china.org/topics/789/laravel-learning-notes-the-magic-of-the-service-container

* https://laravel-china.org/topics/1954/on-laravel-design-pattern
