---
title: PHP Session
date: 2016-10-12 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

`Session` 保存在服务端。保存在超全局变量 `$_SESSION`。

<!--more-->

Session 文件驱动注意 `阻塞` 问题。

# Session 过期

```bash
session.gc_maxlifetime=1440

session.gc_probability=1

session.gc_divisor=1000 # divisor 除数、分母

; 回收概率
```

session.gc_divisor 与 session.gc_probability 合起来定义了在每个会话初始化时启动 gc 进程的概率。此概率用 `gc_probability/gc_divisor` 计算得来。例如 1/100 意味着在每个请求中有 1% 的概率启动 gc 进程。

比如：session.gc_maxlifetime=30，session.gc_divisor=1000，session.gc_probability=1，就表示每一千个用户调用 session_start() 就百分百的会执行一次垃圾回收机制。

* 所以过期 session 是由 gc 处理的，不是自己自动消失的。

* 假设 gc_maxlifetime=120 如果某个 session 文件最后修改时间是 120 秒之前，那么在下一次回收（ 1/100 的概率）发生前，这个 session 仍然是有效的。所以并不是 session 过了有效期，就一定访问不到！

## 严格控制过期时间

* http://www.laruence.com/2012/01/10/2469.html

1. 设置 Cookie 过期时间 30 分钟, 并设置 Session 的 lifetime 也为 30 分钟.

2. 自己为每一个 Session 值增加 Time stamp.

3. 每次访问之前, 判断时间戳.

```php
ini_set('session.gc_maxlifetime', "1800"); // s
ini_set('session.cookie_lifetime', '1800'); // s

if(isset($_SESSION['expiretime'])) {
    if($_SESSION['expiretime'] < time()) {
        unset($_SESSION['expiretime']);
        header('Location: logout.php?TIMEOUT'); // 登出
        exit(0);
    } else {
        $_SESSION['expiretime'] = time() + 3600; // 刷新时间戳
    }
}
```

# 设置 Session

```php
session_start([$options]);

$_SESSION(['username'])='username';

session_write_close();
```

`PHPSESSIONID` 保存在服务端文件中，也将 id 保存在 `Cookie` 中，也可以通过 url 传递。

## 通过 `Cookie` 设置 `Session` 生存期

```php
session_id(); // 设置 session id

session_name(); // 设置 session name，以上两个必须在 start 之前调用。

session_start();

setcookie(session_name(),session_id(),time()+3600)
```

# 传递 Session id
