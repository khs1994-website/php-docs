---
title: PHP 扩展记录
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

扩展列表

* php-reids
* php-memcached
* php-mongodb
* pdo-mysql

# php-reids

第一步：得到扩展文件，第二步：修改 `php.ini` 配置文件，第三步：重启 php-fpm。

## pecl 命令安装

下面列举了一些常用参数，更多参数使用 `pecl help` 查看，注意 `pecl install [ext1] [ext2] ...` 一次可以安装多个扩展。

```bash
$ pecl channel-update pecl.php.net

# 设置

$ pecl config-show

$ pecl config-set php_ini /usr/local/php/etc/php.ini

# 安装扩展

$ pecl install extname

# 测试版

$ pecl install extname-beta

# 指定版本

$ pecl install extname-0.1
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

$ make install
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

# 文件最后增加如下内容,路径根据实际修改

# zend 扩展必须加上绝对路径

extension=/usr/local/php/lib/php/extensions/no-debug-zts-20160303/redis.so

# 根据实际测试，不加路径也是可以的
extension=redis.so
```

## 测试

使用 `phpinfo()` 查看

# php-mongodb

mododb 数据库有两个扩展 `mongo`（已废弃，不支持 PHP7） `mongodb`。

```bash
$ pecl install mongodb
```

# php-memcached

```bash
$ sudo apt install libmemcached-dev

$ pecl install memcached

# 提示 libmemcached directory [no] : 回车跳过即可
```

# pdo-mysql

`PHP` 编译选项 `--with-pdo-mysql` 实现

# 相关链接

* [官方文档](http://php.net/manual/zh/install.pecl.php)

* http://blog.csdn.net/jt521xlg/article/details/47757109
