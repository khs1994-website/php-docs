---
title: Laravel 5 框架基础配置
date: 2017-03-01 11:00:00
updated:
comments: true
tags:
- PHP
- Laravel
categories:
- PHP
- Laravel
---

本文介绍了 Laravle 5 的安装及简要的使用方法。

<!--more-->

# 安装

```bash
$ composer global require "laravel/installer"

$ laravel new blog
```

# 密钥

一般情况下安装程序会自动设置好，如果提示错误，请执行以下命令：

```bash
$ php artisan key:generate
```

# phpredis (pecl)

`config/database.php`

```php
'redis' => [

        //'client' => 'predis',
        'client' => 'phpredis',

        ...
```
