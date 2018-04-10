---
title: Laravel 计划任务
date: 2017-03-11 13:00:00
updated:
comments: true
tags:
- PHP
- Laravel
categories:
- PHP
- Laravel
---

Laravel 计划任务介绍。

<!--more-->

# 准备

`crontab` 增加如下条目。

```bash
* * * * * php /path-to-your-project/artisan schedule:run >> /dev/null 2>&1
```

# 定义任务

在 `App\Console\Kernel` 的 `schedule` 方法中定义。

```php
$schedule->call(function () {
    DB::table('recent_users')->delete();
})->daily();

$schedule->command('emails:send --force')->daily();

$schedule->command(EmailsCommand::class, ['--force'])->daily();

$schedule->job(new Heartbeat)->everyFiveMinutes();

$schedule->exec('node /home/forge/script.js')->daily();
```
