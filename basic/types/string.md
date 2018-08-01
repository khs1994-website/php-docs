---
title: PHP 字符串相关函数
date: 2016-10-6 12:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
- Types
---

本文列举了 PHP 字符串相关函数。

<!--more-->

# 替换

```php
mixed str_replace( mixed $search, mixed $replace , mixed $subject [, int &$count]);
```

`$count` 如果被指定，它的值将被设置为替换发生的次数。

上述函数区分大小写，`str_ireplace()` 不区分大小写。

# 特殊字符相关函数

## 增加反斜线

以 C 语言风格使用反斜线转义字符串中的字符

```php
string addcslashes ( string $str , string $charlist )
```

使用反斜线引用字符串 单引号（'）、双引号（"）、反斜线（\）与 NUL

```php
string addslashes ( string $str )
```

## 去掉反斜线

```php
string stripcslashes ( string $str )
```

`\'` 转换为 `'` 等等

```php
string stripslashes ( string $str )
```

# 单引号

想要输出 `\`，须输入 `echo '\\'`。

`echo '\r';` 等会原样输出。

# 双引号

能够解析特殊字符

```php
echo "$a";

echo "{$a}b"; echo "${a}b"

echo "\$a"; // 使用反斜杠转义

echo "$a[1]"; // 返回字符串中指定位置的字符
```

# heredoc

```php
<<<EOF

$a // 能解析变量

EOF;

<<<"EOF"


EOF;
```

# nowdoc

```php
<<<'EOF'

$a // 不能解析变量

EOF;
```

# 生成随机字符串

```php
/**
* @since 7.1
*/

session_create_id(); // 更好，重复数据出现可能性低
```

* `uniqid()` 可能有重复数据

* https://blog.csdn.net/ghostyusheng/article/details/53788087

# 其他

* 首字母大写/小写 `ucfirst()` `lcfirst()`

* 字符串中每个单词首字母大写 `ucwords('a b c')`
