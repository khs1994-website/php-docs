---
title: LAMP CentOS7 开发环境配置
date: 2016-09-05 12:00:00
updated:
comments: true
tags:
- PHP
- php-dev-env
categories:
- PHP
- php-dev-env
---

本文简要介绍了手动搭建 `LNMP` 开发环境的步骤。

<!--more-->

# Docker

使用 Docker 可以很方便的搭建 LNMP 环境，具体请查看以下链接。

[khs1994-docker/lnmp](https://github.com/khs1994-docker/lnmp)

# Windows

* https://www.khs1994.com/php/development/wnamp.html

# macOS

* https://www.khs1994.com/php/development/mnamp.html

# NGINX

编译安装。

# MySQL

`mysql-community-client-5.7.13-1.el7.x86_64.rpm`  
`mysql-community-common-5.7.13-1.el7.x86_64.rpm`  
`mysql-community-libs-5.7.13-1.el7.x86_64.rpm`  
`mysql-community-server-5.7.13-1.el7.x86_64.rpm`  

```bash
$ rpm -qa | grep mariadb

$ rpm -e --nodeps mariadb-libs-5.5.37-1.el7_0.x86_64

$ yum install *.rpm

$ service mysqld start

$ service mysqld status
```

## 找到初始密码

```bash
$ sudo grep 'temporary password' /var/log/mysqld.log

$ mysql -uroot -p

# 修改密码

$ ALTER USER 'root'@'localhost' IDENTIFIED BY 'NewPassword';
```

## 远程登录

### 添加登录用户

```sql
$  GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' IDENTIFIED BY 'MyPassword' WITH GRANT OPTION;
```

### 修改监听地址

编辑 `/etc/mysql/my.conf` 文件。

```yaml
[mysqld]
bind-address=127.0.0.1 改为 bind-address=0.0.0.0
```

# PHP

该版本为 `PHP7`。

```bash
$ rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

$ yum install php70w-fpm

$ yum install php70w-mysqlnd # PHP与数据库连接
```

## 启动服务

```bash
# 开启 PHP-FPM 服务

$ systemctl start php-fpm.service

# 开机自启动

$ systemctl enable php-fpm.service
```
