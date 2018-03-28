---
title: Laravel 队列
date: 2017-03-12 13:00:00
updated:
comments: true
tags:
- PHP
- Laravel
categories:
- PHP
- Laravel
---

Laravel 队列介绍。

<!--more-->

# 创建

```bash
php artisan make:job SendReminderEmail
```

# 分发

```php
ProcessPodcast::dispatch($podcast);

                ->delay(Carbon::now()->addMinutes(10)); // 延迟分发

                ->onQueue('processing'); // 分发任务到指定队列

                ->onConnection('sqs'); // 指定连接
```
