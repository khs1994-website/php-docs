---
title: PHP 加密函数
date: 2018-06-01 12:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Auth
---

`hash()` `password_hash()`

<!--more-->

```php
hash($algo, $data [, $raw_output])

// algo 加密算法，可以通过 hash_algos() 函数查看

password_hash ( string $password , int $algo [, array $options ] )

// algo 加密算法，通过 PASSWORD_* 常量设置 
```
