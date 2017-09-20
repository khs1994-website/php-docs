---
title: LAMP CentOS7 开发环境配置
date: 2017-05-01 14:00:00
updated:
comments: true
tags:
- PHP
- php-dev-env
categories:
- PHP
- php-dev-env
---

本文简要介绍了手动搭建 LNMP 开发环境的步骤。

<!--more-->

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

$ ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';
```

## 添加远程登录用户

```sql
$  GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' IDENTIFIED BY 'mytest' WITH GRANT OPTION;
```
# MySQL 5.5

```bash
$ vi /etc/mysql/my.conf

[mysqld]
bind-address=127.0.0.1 改为 bind-address=0.0.0.0
```

# PHP

## PHP5

```bash
$ yum install php56u
```

## PHP7

```bash
$ rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
$ yum install php70w
$ yum install php70w-mysqlnd #PHP与数据库连接
```

## PHP-FPM

# 安装PHP-FPM

## PHP5.6版

```bash
$ yum install php56u-fpm
$ systemctl start php-fpm.service #开启PHP-FPM服务
$ systemctl enable php-fpm.service #开机自启动
```
