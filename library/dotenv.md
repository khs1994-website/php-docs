---
title: Dotenv -- PHP .env 转变为 $_ENV
date: 2018-04-11 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Library
---

GitHub：https://github.com/vlucas/phpdotenv

<!--more-->

```bash
$ composer require vlucas/phpdotenv
```

```php
$dotenv = new Dotenv\Dotenv(__DIR__);

# $dotenv = new Dotenv\Dotenv(__DIR__, 'my_env_file_name');

$dotenv->load();
```
