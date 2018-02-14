---
title: PhpStorm 配置 Laravel 智能提示
date: 2017-03-02 13:00:00
updated:
comments: true
tags:
- PHP
- Laravel
categories:
- PHP
- Laravel
---

本文介绍了 PhpStorm 下的 Laravel 智能提示。

<!--more-->

# 配置 composer

设置中搜索 `composer` 进行设置

# 安装 laravel-ide-helper

GitHub：https://github.com/barryvdh/laravel-ide-helper

仅在开发环境中使用

```bash
$ composer require --dev barryvdh/laravel-ide-helper
```

在 `app/Providers/AppServiceProvider.php` 中添加如下内容

```php
public function register()
{
    if ($this->app->environment() !== 'production') {
        $this->app->register(\Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class);
    }
    // ...
}
```

通过命令行生成 `_ide_helper.php` 文件

```bash
$ php artisan ide-helper:generate
$ php artisan ide-helper:meta
$ php artisan optimize
```

在 `.gitignore` 中添加如下内容

```bash
.phpstorm.meta.php
_ide_helper.php
```

# 插件

`Laravel Plugin`
