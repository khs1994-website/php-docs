---
title: Laravel 缓存
date: 2017-03-07 13:00:00
updated:
comments: true
tags:
- PHP
- Laravel
categories:
- PHP
- Laravel
---

Laravel 缓存相关介绍。

<!--more-->

```php

// 配置驱动

Cache::store('redis')->

::get()

::put()

::add()

::has()

::increment()

::decrement()

::pull() // 获取之后删除

::forever()

::forget()

::flush() // 清空，全部删除

::tags()->
```

辅助函数

```php
cache()
```
