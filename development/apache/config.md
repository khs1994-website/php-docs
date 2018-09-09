---
title: Apache 配置
date: 2016-09-11 13:00:00
updated:
comments: true
tags:
- PHP
- HTTPD
categories:
- PHP
- HTTPD
---

本文简要介绍了 `Apache` 配置 `https` 、子域名。

GitHub：https://github.com/khs1994-website/https

<!--more-->

如果启动出现错误，搜索一下错误信息，一般启用某些模块就行了。

# 访问控制

一般出现 403 错误，可能是访问控制出了问题，对照说明检查一下配置。

## 2.2.x

使用 `Order`(排序), `Allow`(允许), `Deny`(拒绝),`Satisfy`(满足)指令来实现。

## 2.4.x

`Require`

## 对比

```apacheconf
Order deny,allow  # 排序，先拒绝后允许
Deny from all     # 拒绝所有

Require all denied # 拒绝所有

Order allow,deny # 排序，先允许后拒绝
Allow from all   # 允许所有

Require all granted # 允许所有

Order Deny,Allow        # 排序，先拒绝后允许
Deny from all           # 拒绝所有
Allow from splaybow.com # 允许 splaybow.com

Require host splaybow.com # 允许 splaybow.com
```

```apacheconf
Require all granted             # 允许所有来源访问

Require all denied              # 拒绝所有来源访问

Require expr expression         # 允许表达式为true时访问

Require ip 10 172.20 192.168.2  # 允许特定IP段访问，多个段之前用空格隔开。每个段使用开头几项表示

Require host splaybow.com       # 只允许来自域名splaybow.com的主机访问
```

## 参考资料

* http://www.splaybow.com/post/apache-forbidden-directory-require.html

# https

修改主配置文件 `/usr/local/apache2/conf/httpd.conf`

```apacheconf
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so

LoadModule ssl_module modules/mod_ssl.so
```

为了方便这里不启用 `/usr/local/apache2/conf/extra/httpd-ssl.conf`

直接在 `/usr/local/apache2/conf/extra/httpd-vhosts.conf` 增加内容

```apacheconf
Listen 443

SSLCipherSuite HIGH:MEDIUM:!MD5:!RC4:!3DES
SSLProxyCipherSuite HIGH:MEDIUM:!MD5:!RC4:!3DES

SSLHonorCipherOrder on

SSLProtocol all -SSLv3
SSLProxyProtocol all -SSLv3

SSLSessionCache        "shmcb:/usr/local/apache2/logs/ssl_scache(512000)"
SSLSessionCacheTimeout 300
```

# 多主机配置

修改主配置文件 `/usr/local/apache2/conf/httpd.conf`

```apacheconf
# Virtual hosts 取消注释
Include conf/extra/httpd-vhosts.conf
```

修改子配置文件 `/usr/local/apache2/conf/extra/httpd-vhosts.conf`

基于 域名、IP、端口来实现多主机，具体看示例配置。

不建议使用以上方式，参考 NGINX 配置方式，我们可以把某一个目录中全部的 `*.conf` 文件包含进来。

```apacheconf
Include conf/conf.d/*.conf
```

一个虚拟主机一个文件（`conf/conf.d/*.conf`）。

# 目录列表

是否显示目录列表

```apacheconf
<Directory "/app">

Options Indexes FollowSymLinks

<Directory "/app">
```

# 重写

```apacheconf
<Directory "/app">

AllowOverride None
AllowOverride All
AllowOverride FileInfo AuthConfig Limit

<Directory "/app">
```
