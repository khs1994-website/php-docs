---
title: Apache 配置
date: 2016-09-11 13:00:00
updated:
comments: true
tags:
- PHP
- php-dev-env
- Apache
categories:
- PHP
- php-dev-env
- Apache
---

本文简要介绍了 `Apache` 配置 `https` 、子域名。

<!--more-->

如果启动出现错误，搜索一下错误信息，一般启用某些模块就行了。

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

更多配置详情：https://github.com/khs1994-docker/lnmp-nginx-apache2-demo/blob/master/httpd-vhosts.conf

# 多域名配置

修改主配置文件 `/usr/local/apache2/conf/httpd.conf`

```apacheconf
# Virtual hosts
Include conf/extra/httpd-vhosts.conf
```

修改子配置文件 `/usr/local/apache2/conf/extra/httpd-vhosts.conf`

```apacheconf
Listen 8080
```

## 官方示例配置

```apacheconf
<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host.example.com
    DocumentRoot "/usr/local/apache2/docs/dummy-host.example.com"
    ServerName dummy-host.example.com
    ServerAlias www.dummy-host.example.com
    ErrorLog "logs/dummy-host.example.com-error_log"
    CustomLog "logs/dummy-host.example.com-access_log" common
</VirtualHost>

<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host2.example.com
    DocumentRoot "/usr/local/apache2/docs/dummy-host2.example.com"
    ServerName dummy-host2.example.com
    ErrorLog "logs/dummy-host2.example.com-error_log"
    CustomLog "logs/dummy-host2.example.com-access_log" common
</VirtualHost>
```

## 实际配置

### 403 错误

```apacheconf
<Directory "/var/www/html">
    #
    # Possible values for the Options directive are "None", "All",
    # or any combination of:
    #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
    #
    # Note that "MultiViews" must be named *explicitly* --- "Options All"
    # doesn't give it to you.
    #
    # The Options directive is both complicated and important.  Please see
    # http://httpd.apache.org/docs/2.4/mod/core.html#options
    # for more information.
    #
    Options Indexes FollowSymLinks

    #
    # AllowOverride controls what directives may be placed in .htaccess files.
    # It can be "All", "None", or any combination of the keywords:
    #   AllowOverride FileInfo AuthConfig Limit
    #
    AllowOverride None

    #
    # Controls who can get stuff from this server.
    #
    Require all granted
</Directory>
```

### 基于端口

```apacheconf
<VirtualHost *:8080>
      ServerAdmin khs1994@khs1994.com
      DocumentRoot "/var/www/html"
      ServerName khs1994.com

      ErrorLog "logs/khs1994.com-error_log"
      CustomLog "logs/khs1994.com-access_log" common

      # https 跳转
      RewriteEngine on
      RewriteCond %{HTTP_HOST} !^khs1994.com[NC]
      RewriteRule ^(.*)$ http://www.khs1994.com$1 [L,R=301]


      # 403 错误  
      <Directory "/app/test" >
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
      </Directory>
</VirtualHost>
```

### 基于 IP

```apacheconf
<VirtualHost *:80>
      ServerAdmin khs1994@khs1994.com
      DocumentRoot "/var/www/html"
      ServerName www.khs1994.com
      ErrorLog "logs/www.khs1994.com-error_log"
      CustomLog "logs/www.khs1994.com-access_log" common

      RewriteEngine on
      RewriteCond %{SERVER_PORT} !^443$
      RewriteRule ^(.*)?$ https://%{SERVER_NAME}$1 [L,R]
</VirtualHost>
```

### 基于域名

```apacheconf
<VirtualHost *:80>
      ServerAdmin khs1994@khs1994.com
      DocumentRoot "/var/www/bbs"
      ServerName bbs.khs1994.com
      ErrorLog "logs/bbs.khs1994.com-error_log"
      CustomLog "logs/bbs.khs1994.com-access_log" common
</VirtualHost>
```
