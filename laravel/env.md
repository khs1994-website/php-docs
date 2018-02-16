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

* 测试: `testing` （运行 `PHPUnit` 使用该 .env 文件）

* 预上线: `staging`

* 正式环境: `production`


生产环境加载 `.env.production`

以此类推

# 在 `php-fpm.d/www.conf` 配置环境变量

```yaml
env[APP_ENV]=development;

env[APP_ENV]=production;
```

# 也可以设置系统环境变量

`/etc/profile` 文件末尾写入以下内容

```bash
export APP_ENV=development

# export APP_ENV=production
```

注意将 `php.ini` 中的选项改为：

```bash
;variables_order = "GPCS"

variables_order = "EGPCS"
```

# 验证

查看 `phpinfo()` 页面，搜索查看 `APP_ENV` 与预设环境相匹配即可。

# More Information

* https://laravel-china.org/articles/5638/laravel-env-the-loading-of-environment-variables-and-source-code-analysis

* https://segmentfault.com/a/1190000009682704
