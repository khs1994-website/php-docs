---
title: PHP 流程控制
date: 2016-10-18 13:00:00
updated:
comments: true
tags:
- PHP
categories:
- PHP
- Basic
---

PHP 流程控制简介。

* http://php.net/manual/zh/language.control-structures.php

<!--more-->

```php
if (condition) {
  # code...
}

if (condition) {
  # code...
} else {
  # code...
}
```

```php
switch (variable) {
  case 'value':
    # code...
    break;

  default:
    # code...
    break;
}
```

```php
while ($a <= 10) {
  # code...
}
```

```php
do {
  # code...
} while ($a <= 10);
```

```php
for ($i=0; $i < ; $i++) {
  # code...
}
```

```php
foreach ($variable as $key => $value) {
  # code...
}
```

```php
goto a;
echo 'Foo';

a:
echo 'Bar';

// 结果 Bar
```
