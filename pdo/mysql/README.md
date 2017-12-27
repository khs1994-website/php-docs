---
title: PHP PDO MySQL
date: 2017-04-02 13:00:00
updated:
comments: true
tags:
- PHP
- PDO
- MySQL
categories:
- PHP
- PDO
- MySQL
---

# 连接

```php
# 数据源
$dsn='mysql:host=localhost;dbname=imooc';

# $dsn='uri:file//G:\path'

...

$pdo=new PDO($dsn,$username,$password);

var_dump($pdo);
```
