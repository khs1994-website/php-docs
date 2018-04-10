---
title: PHP 扩展安装配置
date: 2016-09-23 16:00:00
updated:
comments: true
tags:
- PHP
- php-dev-env
categories:
- PHP
- php-dev-env
---

本文记录 PHP 扩展及其简单安装方法。

<!--more-->

# 修订记录

* PHP 7.2+  **php.ini** 中扩展的配置写法发生了变化

# 依赖

安装扩展时可能需要安装一些依赖库，查询出错信息，安装对应的依赖库即可。

# 总体步骤

第一步：得到扩展文件（Linux 编译 / Linux pecl install / Windows 直接下载）

第二步：修改 `php.ini` 配置文件

第三步：重启 php-fpm。

## pecl install

下面列举了一些常用参数，更多参数使用 `pecl help` 查看，注意 `pecl install [ext1] [ext2] ...` 一次可以安装多个扩展。

以下命令可能需要加上 `sudo`

```bash
$ sudo pecl channel-update pecl.php.net

# 设置

$ sudo pecl config-show

# pecl pear 同时设置了 ini 路径才能在使用 pecl 安装扩展时自动生成配置

$ sudo pecl config-set php_ini /usr/local/php/etc/php.ini
$ sudo pear config-set php_ini /usr/local/php/etc/php.ini

# 安装扩展

$ sudo pecl install extname

# 测试版

$ sudo pecl install extname-beta

# 指定版本

$ sudo pecl install extname-0.1
```

## 编译安装

请在 http://pecl.php.net 搜索下载  

安装 `autoconf` 等软件

```bash
$ wget http://pecl.php.net/get/redis-3.1.2.tgz

# 解压、进入

$ phpize

$ ./configure --with-php-config=/usr/local/php/bin/php-config

$ make

$ sudo make install
```

通过以上两种方法得到扩展文件，查看：

```bash
$ cd /usr/local/php/lib/php/extensions/no-debug-zts-20160303
```

在里边可以看到 `redis.so` 文件

其他扩展的 `编译安装` 方法类似，这里不再介绍。

## 修改配置文件

```bash
$ vi /usr/locla/php/etc/php.ini

# 注意 php.ini 中只能使用 ; 注释

# 文件最后增加如下内容,扩展不在默认编译路径（ext 指令设置的路径），请填写绝对路径

#
# 格式 extension=<ext>
#
# @since 7.2
# @link  https://github.com/khs1994-php/ini/compare/7.1.0...7.2.0#diff-93ba055b6b5afa0ffd531ce1ff45508aR874
#

extension=redis

# 旧的，未来可能废弃的写法
#
# extension=redis.so
#
# extension=php_redis.dll (Windows)
#

# zend 扩展，例如 xdebug opcache ,格式为 zend_extension=<ext> ，请不要与普通扩展混淆
# 注意替换为自己的实际路径，每个 PHP 版本目录名可能不同

zend_extension=xdebug

# zend_extension=c:/php-ext/php_xdebug
```

## 验证

使用 `phpinfo()` 查看或 `$ php -m`

# 其他扩展

简要说明一下

## php-mongodb

mododb 数据库有两个扩展 `mongo`（已废弃，不支持 PHP7） `mongodb`。

```bash
$ sudo pecl install mongodb
```

## php-memcached

```bash
$ sudo apt install libmemcached-dev

$ sudo pecl install memcached

# 提示 libmemcached directory [no] : 回车跳过即可
```

## pdo-mysql

`PHP` 编译选项添加 `--with-pdo-mysql`

# 相关链接

* [官方文档](http://php.net/manual/zh/install.pecl.php)

* http://blog.csdn.net/jt521xlg/article/details/47757109
