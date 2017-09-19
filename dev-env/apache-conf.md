---
title: Apache 配置
date: 2017-05-01 13:00:00
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

# https

## 子配置文件
`/usr/local/apache/conf/extra/httpd-ssl.conf`

<!--more-->

```apacheconf
<VirtualHost _default_:443>
   DocumentRoot "/var/www/t"
    ServerName a.khs1994.com:443

    ErrorLog logs/ssl_error_log
    TransferLog logs/ssl_access_log
    LogLevel warn
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5

    SSLCertificateFile /etc/httpd/conf/1_a.khs1994.com_cert.crt
    SSLCertificateKeyFile /etc/httpd/conf/2_a.khs1994.com.key

    <Files ~ "\.(cgi|shtml|phtml|php3?)$">
      SSLOptions +StdEnvVars
    </Files>
    <Directory "/var/www/cgi-bin">
      SSLOptions +StdEnvVars
      </Directory>
      BrowserMatch "MSIE [2-5]" \
          nokeepalive ssl-unclean-shutdown \
          downgrade-1.0 force-response-1.0
          CustomLog logs/ssl_request_log \
          "%t %h %{SSL_PROTOCOL}x %{SSL_CIPHER}x \"%r\" %b"
</VirtualHost>  

SSLEngine off
```
# 多域名配置

## 主配置文件修改

`/usr/local/apache/conf/httpd.conf`

```apacheconf
# 多端口监听
Listen 80
Listen 8080
# 去掉 # 号
# Virtual hosts
Include conf/extra/httpd-vhosts.conf
```

## 子配置文件

`/usr/local/apache/conf/extra/httpd-vhosts.conf`

### 官方示例配置

```apacheconf
<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host.example.com
    DocumentRoot "/usr/local/apache/docs/dummy-host.example.com"
    ServerName dummy-host.example.com
    ServerAlias www.dummy-host.example.com
    ErrorLog "logs/dummy-host.example.com-error_log"
    CustomLog "logs/dummy-host.example.com-access_log" common
</VirtualHost>

<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host2.example.com
    DocumentRoot "/usr/local/apache/docs/dummy-host2.example.com"
    ServerName dummy-host2.example.com
    ErrorLog "logs/dummy-host2.example.com-error_log"
    CustomLog "logs/dummy-host2.example.com-access_log" common
</VirtualHost>
```

### 实际配置

`基于端口` `基于IP` `基于域名`

```apacheconf
<VirtualHost *:8080>
      ServerAdmin khs1994@khs1994.com
      DocumentRoot "/var/www/html"
# 出现 403 错误增加以下内容，第一行路径注意修改    
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

      ServerName khs1994.com
      ErrorLog "logs/khs1994.com-error_log"
      CustomLog "logs/khs1994.com-access_log" common
      #https跳转
      RewriteEngine on
      RewriteCond %{HTTP_HOST} !^khs1994.com[NC]
      RewriteRule ^(.*)$ http://www.khs1994.com$1 [L,R=301]
</VirtualHost>
```

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

```apacheconf
<VirtualHost *:80>
      ServerAdmin khs1994@khs1994.com
      DocumentRoot "/var/www/bbs"
      ServerName bbs.khs1994.com
      ErrorLog "logs/bbs.khs1994.com-error_log"
      CustomLog "logs/bbs.khs1994.com-access_log" common
</VirtualHost>
```
