---
title: PHP 依赖管理工具 Composer
date: 2016-11-25 12:00:00
updated:
comments: true
tags:
- PHP
- Composer
categories:
- PHP
- Composer
---

GitHub：https://github.com/composer/composer

官方网站：https://getcomposer.org/

<!--more-->

# 版本表示方法

https://cuiqingcai.com/3494.html

* `~` `~1.2` 相当于 `>=1.2 <2.0.0` 而 `~1.2.3` 相当于 `>=1.2.3 <1.3.0`

* `^` `^1.2.3` 相当于 `>=1.2.3 <2.0.0` 1.0 以下较特殊 `^0.3` 会被当作 `>=0.3.0 <0.4.0`

# 安装

## 下载地址

* https://getcomposer.org/download/

* https://github.com/composer/composer/releases

下载之后移入 `PATH` (`/usr/local/bin`)，改名为 `composer`

## 中国镜像

```bash
$ composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

* https://pkg.phpcomposer.com/

## macOS

```bash
$ brew install composer
```

# 开发一个 SDK

GitHub：https://github.com/khs1994-docker/php-demo

```bash
$ composer create-project --prefer-dist khs1994/example sdk @dev
```

## GitHub 设置

git 仓库设置中 `Integration & services` 中搜索添加 `Packagist`。

`Token` 在 https://packagist.org/profile/ 中查看

`Domain` 为 https://packagist.org

# 在项目中使用

```bash
$ composer require khs1994/qq-login @dev

# 只在开发环境使用某包

$ composer require --dev phpunit/phpunit
```

## 自动加载

```php
<?php

require __DIR__."/vendor/autoload.php";

```

## `dist` 和 `源码`

`dist` 是打包版本 `--prefer-dist`

想要克隆源码加上 `--prefer-source`
