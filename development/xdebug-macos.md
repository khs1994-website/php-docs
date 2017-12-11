---
title: macOS PhpStorm Xdebug 使用详解
date: 2017-03-05 12:00:00
updated:
comments: true
tags:
- PHP
- PhpStorm
categories:
- PHP
- IDE
---

# 场景

* LNMP 位于 macOS
* LNMP 位于 Docker
* LNMP 位于虚拟机中的 Dcoker

<!--more-->

# php-xdebug

## 安装

```bash
# php也是通过brew安装的

$ brew info php71-xdebug
$ brew install php71-xdebug
```

## 配置

`/usr/local/etc/php/7.1/conf.d/ext-xdebug.ini`

```ini
[xdebug]
zend_extension="/usr/local/opt/php71-xdebug/xdebug.so"
xdebug.remote_enable=1
#xdebug.remote_host=local004.khs1994.com
xdebug.remote_connect_back=1
xdebug.remote_port=9010
xdebug.remote_log=/tmp/xdebug-remote.log
xdebug.remote_handler=dbgp
```

# Chrome 插件

`xdebug helper`,在选项中选择 `PhpStrom`

# PhpStrom 配置

* `File -> Settings -> Languages&Frameworks -> PHP -> Debug ->Xdebug` `Debug port:` 9010 三个选项全部勾选（必须与扩展中配置的端口一致）。

# 使用

* 设置断点  
* 点击`电话`图标(run->Start listening for PHP...)  
* chrome打开网址，点击 `xdebug helper` -》`debug` ,自动跳转到IDE

# 相关链接

* http://blog.csdn.net/willcold/article/details/68068090
* https://segmentfault.com/a/1190000005878593
* http://blog.csdn.net/u012914309/article/details/65440609
