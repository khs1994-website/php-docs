---
title: PHP 执行 Shell 命令
date: 2016-10-14 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

主要有 `exec()` `shell_exec()` `system()`。

<!--more-->

# `exec()`

```php
string exec ( string $command [, array $output [, int $return_var ]] )
```

返回最后一条结果。

如果使用了 `output` 参数，shell 命令的每行结果会填充到该数组中。

# `shell_exec()`

```php
string shell_exec(string $cmd)
```

以 `字符串` 形式返回执行的全部结果。

# `system()`

```php
string system(string $command [, int $return_value])
```

输出全部结果。

成功则返回命令输出的最后一行， 失败则返回 `FALSE`

# 反引号

反引号不能在双引号字符串中使用。

```php
echo `ls`;
```

# 其他

请查看：http://php.net/manual/zh/ref.exec.php
