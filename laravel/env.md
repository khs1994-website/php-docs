---
title: Laravel 环境变量
date: 2017-10-03 13:00:00
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

* 开发: development

* 测试: testing

* 预上线: staging

* 正式环境: production


生产环境加载 `.env.production`

开发环境加载 `.env.development`

在 `php-fpm.d/www.conf` 添加环境变量

```yaml
env[APP_ENV]=development;
env[APP_ENV]=production;
```

也可以设置系统环境变量( Docker 中可以直接设置环境变量，本机不行，这里不再探讨)。

查看 `phpinfo()` 页面，搜索查看 `Environment` 与预设环境相匹配即可。

# More Information

* https://laravel-china.org/articles/5638/laravel-env-the-loading-of-environment-variables-and-source-code-analysis

* https://segmentfault.com/a/1190000009682704
