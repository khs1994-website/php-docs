---
title: Laravel 环境变量
date: 2017-03-03 13:00:00
updated:
comments: true
tags:
- PHP
- Laravel
categories:
- PHP
- Laravel
---

不同环境加载不同的 `.env` 文件。

<!--more-->

* 开发: `development`

* 测试: `testing` （运行 `PHPUnit` 使用 `.env.testing` 文件）

* 预上线: `staging`

* 正式环境: `production`


生产环境加载 `.env.production`

以此类推

# 设置系统环境变量

`/etc/profile` 文件末尾写入以下内容

```bash
export APP_ENV=development

# export APP_ENV=production
```

Windows 不再赘述。

# 验证

```bash
$ php artisan env

Current application environment: development
```

与上一步系统变量一致说明设置成功，Windows 设置系统变量之后记得注销再登陆。

# More Information

* https://laravel-china.org/articles/5638/laravel-env-the-loading-of-environment-variables-and-source-code-analysis

* https://segmentfault.com/a/1190000009682704
