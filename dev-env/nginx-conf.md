---
title: Nginx 配置
date: 2017-05-04 13:00:00
updated:
comments: true
tags:
- php-dev-env
- Nginx
categories:
- PHP
- php-dev-env
- Nginx
---

本文详细介绍了 nginx 常用配置。

<!--more-->

修改主配置文件 `/etc/nginx/nginx.conf`

```nginx

worker_processes  auto;

http {
  # 引入子配置文件
  index index.php index.htm index.html;
  # 配置 index
  include /etc/nginx/conf.d/*.conf;
  # 将 sever 块内容全部注释
}
```

# 命令

```bash
# stop是快速停止nginx，可能并不保存相关信息，quit是完整有序的停止nginx，并保存相关信息
$ nginx -s stop
$ nginx -s quit
# 重新打开日志文件命令
$ nginx -s reopen
# 重新载入配置文件
$ nginx -s reload
```

# PHP

```nginx
server{
  location ~ \.php$ {
      root           /var/www2/www;
      fastcgi_pass   phpfpm:9000;
      fastcgi_index  index.php;
      fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
      include        fastcgi_params;
  }
}
```

# default_server

```nginx
server {
    listen       80  default_server;
    server_name  oschina.net  www.oschina.net;
}       
```

listen 指令后面有一个参数 `default_server` ，这个参数是在 0.8.21 版本以后才有的，而之前是 default 指令。Nginx的虚拟主机是通过 HTTP 请求中的 Host 值来找到对应的虚拟主机配置，如果找不到，那 Nginx 就会将请求送到指定了 `default_server` 的节点来处理，如果没有指定为 `default_server` 的话，就跑到 localhost 的节点，如果没有 localhost 的节点，那只好 404 了。

# 目录浏览功能

Nginx 默认是不允许列出整个目录的。如需此功能，在配置文件中 server 或 location 段里添加上 `autoindex on;` 来启用目录浏览。

```nginx
autoindex on;
#默认为on，显示出文件的确切大小，单位是bytes。改为off后，显示出文件的大概大小，单位是kB或者MB或者GB
autoindex_exact_size off;
#默认为off，显示的文件时间为GMT时间。改为on后，显示的文件时间为文件的服务器时间
autoindex_localtime on;
```

# 负载均衡

```nginx
upstream fzjh {
    server 111.206.227.118 weight=2;
    server 123.206.62.18;
}
server {
    listen 80;
    server_name f.khs1994.com;
    location / {
      proxy_pass http://fzjh;
    }
}
```

# 相关链接

* http://blog.csdn.net/benbendy1984/article/details/6025663
* http://nginx.org/en/docs/http/ngx_http_autoindex_module.html
* [中文文档](https://github.com/oopsguy/nginx-docs)
