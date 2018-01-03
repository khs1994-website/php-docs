---
title: PHP 依赖管理工具 Composer
date: 2016-12-02 12:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
---

# 开发一个 SDK

```json
{
  "name": "khs1994/qq-login",
  "description": "QQ Login SDK",
  "keywords": [
    "qq",
    "oauth"
  ],
  "homepage": "https://github.com/khs1994-php/qq-login",
  "type": "library",
  "license": "MIT",
  "authors": [{
    "name": "khs1994",
    "email": "khs1994@khs1994.com",
    "homepage": "https://khs1994.com"
  }],
  "require": {
    "php": ">=7.0"
  },
  "require-dev": {
    "phpunit/phpunit": "~4.0|~5.0"
  },
  "autoload": {
    "psr-4": {
      "QQLogin\\": "src/QQLogin/"
    }
  }
}
```

## GitHub 设置

git 仓库设置中 `Integration & services` 中搜索添加 `Packagist`。

`Token` 在 https://packagist.org/profile/ 中查看

`Domain` 为 https://packagist.org

# 在项目中使用

```json
{
  "require":{
    "khs1994/qq-login":"*"
  }
}
```

之后引入

```bash
$ composer install | update
```

或使用命令行

```bash
$ composer require "khs1994/qq-login:dev-master"
```

## 自动加载

```php
<?php
require 'vendor/autoload.php';

...
```

## `dist` 和 `源码`

`dist` 用于加了 `tag` 的版本。

想要克隆源码加上 `--prefer-source`
