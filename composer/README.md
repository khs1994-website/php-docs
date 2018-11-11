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

* http://docs.phpcomposer.com/04-schema.html#Root-Package

<!--more-->

# 版本表示方法

https://cuiqingcai.com/3494.html

* `~1.2` `^1.2` 没有区别

* `~` `~1.2` 相当于 `>=1.2 <2.0.0` 而 `~1.2.3` 相当于 `>=1.2.3 <1.3.0`

* `^` `^1.2.3` 相当于 `>=1.2.3 <2.0.0` 1.0 以下较特殊 `^0.3` 会被当作 `>=0.3.0 <0.4.0`

# 稳定性标志

* `dev`、`alpha`、`beta`、`RC`、`stable`

# 本地开发

从 本地 路径加载

```json
"repositories":{
  "tilte": {
    "type":"path",
    "url":"/path/my-package"
  }
}
```

# 从 VCS 加载包

```json
{
    "repositories": [
        {
            "type": "composer",
            "url": "http://packages.example.com"
        },
        {
            "type": "composer",
            "url": "https://packages.example.com",
            "options": {
                "ssl": {
                    "verify_peer": "true"
                }
            }
        },
        {
            "type": "vcs",
            "url": "https://github.com/Seldaek/monolog"
        },
        {
            "type": "pear",
            "url": "http://pear2.php.net"
        },
        {
            "type": "package",
            "package": {
                "name": "smarty/smarty",
                "version": "3.1.7",
                "dist": {
                    "url": "http://www.smarty.net/files/Smarty-3.1.7.zip",
                    "type": "zip"
                },
                "source": {
                    "url": "http://smarty-php.googlecode.com/svn/",
                    "type": "svn",
                    "reference": "tags/Smarty_3_1_7/distribution/"
                }
            }
        }
    ]
}
```

# 安装

## 下载地址

* https://getcomposer.org/download/

* https://github.com/composer/composer/releases

下载之后移入 `PATH` (`/usr/local/bin`)，改名为 `composer`

## 中国镜像

注意关注镜像网站，部分镜像可能不可用

```bash
# 不可用
$ composer config -g repo.packagist composer https://packagist.phpcomposer.com

$ composer config -g repo.packagist composer https://packagist.laravel-china.org
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

> 之前在 github 添加 service 的方法已经废弃，请 PHPer 注意按以下方法升级

首先在 https://github.com/settings/applications 把 `Packagist` Revoke 掉。

之后在 https://packagist.org 选择 github 账号登录，授予权限的时候注意将 **GitHub 组织(如果有的话)** 的权限一并勾选。

在 My packages 界面没有看到警告即可。

* https://packagist.org/about#how-to-update-packages

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
