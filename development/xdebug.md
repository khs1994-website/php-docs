---
title: PhpStorm Xdebug 使用详解
date: 2017-03-05 12:00:00
updated:
comments: true
tags:
- PHP
- PHPer
categories:
- PHP
---

# 场景

* LNMP 位于 本机

* LNMP 位于 Docker 或 WSL

* LNMP 位于虚拟机（远程）

* LNMP 位于虚拟机中的 Docker

<!--more-->

# php xdebug 扩展

## 安装

```bash
# php 也是通过 brew 安装的，已安装的请跳过

$ brew install php

$ pecl install xdebug

# 可能需要修改配置文件来增加扩展，这里不再赘述
```

## 配置

`/usr/local/etc/php/7.2/conf.d/ext-xdebug.ini`

> 注意请替换为实际的路径

```ini
[xdebug]

# 或者填绝对路径

zend_extension="xdebug.so"

xdebug.remote_enable=1
#xdebug.remote_host=local004.khs1994.com
xdebug.remote_connect_back=1
xdebug.remote_port=9010
xdebug.remote_log=/tmp/xdebug-remote.log
xdebug.remote_handler=dbgp
```

# 浏览器插件

## Chrome 插件

https://github.com/mac-cain13/xdebug-helper-for-chrome

在选项中选择 `PhpStrom`

## FireFox 插件

https://github.com/BrianGilbert/xdebug-helper-for-firefox

在选项中选择 `PhpStrom`

# PhpStrom 配置

* `File -> Settings -> Languages&Frameworks -> PHP -> Debug ->Xdebug` `Debug port:` 9010 三个选项全部勾选（必须与扩展中配置的端口一致）。

# 使用

* 设置断点

* 点击 `电话` 图标(run -> Start listening for PHP...)

* 浏览器打开网址，点击 `xdebug helper` -》`debug` ,自动跳转到 IDE

# 相关链接

* http://blog.csdn.net/willcold/article/details/68068090

* https://segmentfault.com/a/1190000005878593

* http://blog.csdn.net/u012914309/article/details/65440609
