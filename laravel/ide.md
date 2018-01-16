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

GitHub地址：https://github.com/barryvdh/laravel-ide-helper

```bash
$ composer require barryvdh/laravel-ide-helper
```

`config/app.php` 中 `providers` 中添加以下内容

```bash
Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,
```

通过命令行生成 `_ide_helper.php` 文件

```bash
$ php artisan ide-helper:generate
```

# 插件

`Laravel Plugin`
