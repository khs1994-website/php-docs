---
title: macOS PhpStorm Docker 使用详解
date: 2017-08-31 12:00:00
updated:
comments: true
tags:
- PHP
- PhpStorm
categories:
- PHP
- IDE
---

在 `PhpStorm | Preferences | Build, Execution, Deployment | Docker` 设置 Docker。

<!--more-->

项目根目录编写 `Dockerfile` `docker-compose.yml`

点击 `Run | Edit configurations` 中添加 `Docker Deployment`

在 `Deployment` 选择 `image` 或者 `Dockerfile` 或者 `docker-compose.yml`

在 `Container` 设置运行命令、挂载数据、端口号等。

# 相关链接

* https://www.jetbrains.com/help/phpstorm/docker-2.html?search=docker
* https://confluence.jetbrains.com/display/PhpStorm/Docker+Support+in+PhpStorm
