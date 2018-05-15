---
title: Doctrine Cache -- PHP 缓存库
date: 2018-04-12 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Library
---

GitHub：https://github.com/doctrine/cache

官方文档：http://doctrine-orm.readthedocs.io/projects/doctrine-orm/en/latest/reference/caching.html

<!--more-->

```bash
$ composer require "doctrine/cache"
```

```php
$cache = new FilesystemCache(sys_get_temp_dir());

$cache->save('k', 'v', $expire_time);
```
