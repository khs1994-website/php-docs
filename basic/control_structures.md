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

PHP 流程控制

* http://php.net/manual/zh/language.control-structures.php

<!--more-->

```php
$a = 0;

switch ($a){ // switch(true)
  case $a >= 0:
  echo 0;
  break;
  case $a >=10:
  echo 1;
  break;
  default:
  echo 2;
  break;
}

exit();
```

结果为 1。switch($a) 实际为 switch(false)，所以匹配 false

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
