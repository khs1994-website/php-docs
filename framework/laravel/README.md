---
title: Laravel 5 框架基础配置
date: 2017-03-01 11:00:00
updated:
comments: true
tags:
- PHP
- Laravel
categories:
- PHP
- Framework
- Laravel
---

本文介绍了 Laravle 5 的安装及简要的使用方法。

<!--more-->

# 生产环境优化

```bash
$ php artisan config:cache   # 配置缓存
$ php artisan route:cache    # 路由缓存
$ php artisan down | up      # 启用或关闭维护模式
```

# 安装

```bash
$ composer global require "laravel/installer"

$ laravel new blog   // laravel 命令只能安装主线版本
```

## 安装特定版本

```bash
$ composer create-project --prefer-dist laravel/laravel=5.5.* blog
```

# 密钥

一般情况下安装程序会自动设置好，如果提示错误，请执行以下命令：

```bash
$ php artisan key:generate
```

# phpredis (pecl)

`config/database.php`

```php
'redis' => [

        //'client' => 'predis',
        'client' => 'phpredis',

        ...
]
```

# 禁用 CSRF 保护

`app\Http\Kernel.php`

注释掉以下几行。

```php
App\Http\Middleware\VerifyCsrfToken
```

# 其他

在 `./config/app.php` 中 `aliases` 过的类，直接 use 类名，不要 use 完整路径。

```php
use App; // 推荐

use Illuminate\Support\Facades\App; // 不推荐
```

## 辅助函数

通过使用函数实现功能

```php
cache(['key'=>1], 5); // 在数组中设置值

cache('ket');         // 获取值

session(['key'=>1]); // 设置值

session('key');
```

## Facades

通过调用类的静态方法实现功能。

```php
Cache::set('key', 'value', 5);

Cache::get('key');

Session::all();
```

## Contracts 契约

# 路由

```php
Route::get();

Route::match(['get'],)

Route::redirect();  // 重定向

Route::view();      // 返回视图

Route::get('/user/{name}/id/{id}',) // url 参数

Route::get('/id/{id?}',function($id){
  return $id;
}); // url 参数的

Route::get()->name('name'); // 路由命名

Route::get()->where(); // 正则表达式约束路由参数

Route::domain('sub.domain.com')->group(function(){

}); // 子域名

Route::prefix('sub')->group(function(){

}); // 路由前缀

Route::namespace('Admin')->group(function(){
    // 在 "App\Http\Controllers\Admin" 命名空间下的控制器
});

Route::middleware()->group(function(){
    // 中间件
});
```

# 中间件

`app\Http\Middleware`

```php
// 新建中间件类

public function handle($request, Closure $next)
{
    // 前置中间件

    // 执行动作

    return $next($request);

    // 后置中间件

    $response = next($request);

    // 执行动作

    return $response;
}
```

## 注册中间件

`app\Http\Kernel`

```php
protected $middleware =[
  // 在这里增加一个条目
];
```

# 控制器

`__invoke` 魔术方法来定义单个控制器。

```php
public function __construct(){
  $this->middleware('auth')
       ->only('method')
       ->except('method');

  $this->middleware(function($request, Closure $next){

      // code

      return $next($request);
  });
}
```

# 响应

```php
$response($content)
    ->header('Content-Type',$type)

    ->withHeaders([ // 数组形式
      'Content-Type'=>$type
    ]);

    ->cookie('key','value','过期时间'); // 参数与原生参数相同

    ->view(); // 响应视图

    ->json([ // 响应 json,直接 return [] 默认返回 json

    ]);

    ->download($filePath); // 强制用户下载指定路径的文件

    ->file($filePath); // 浏览器显示文件（不下载），例如图片、PDF

// 重定向

redirect('routeName')
    ->with() // 数据闪存到 session 中
    ->action('name',[
         // 参数
    ]); // 重定向到 控制器
    ->route('routeName'); // 重定向到路由
```

# 日志

```php
Log::emergency($message);
Log::alert($message);
Log::critical($message);
Log::error($message);
Log::warning($message);
Log::notice($message);
Log::info($message);
Log::debug($message);
```

# 文件

```php
$request->file('photo'); // ->photo; 也可以直接通过文件名调用
        ->hasFile('photo'); // 请求是否包含某文件
        ->isValid(); // 验证文件是否有效
        ->path();      // 文件路径
        ->extension(); // 文件扩展名
        ->store('images'); // 目录名，文件名会自动生成
        ->storeAs('images', 'filename.jpg'); // 指定目录及文件名
```

# Session

```php
Illuminate\Http\Request 实例

->session()->get(); // 获取

           ->put(); // 新增

           ->forget(); // 删除

           ->flush(); // 清空

           ->pull(); // 取值之后删除

           ->flash(); // 闪存

// 辅助函数

session();

// 辅助函数新增值

session(['key'=>1])
```

# Cookie

```php
Illuminate\Http\Request 实例

->cookie('key'); // 获取 cookie

// 辅助函数设置 cookie，生成的是 cookie 实例，之后附加到响应。

$a=cookie(); // 与 PHP 原生 setcookie() 参数一致

return response()->cookie($a);

// 响应时设置 cookie

return response()->cookie(
  'name', 1 , 100
);
```

# 文件系统

建立链接 `storage/app/public` -> `public/storage`

```bash
$ php artisan storage:link
```

```php
Storage::disk('local')->

// 默认路径为 storage/app

       ::put('public/1.txt', 1); // 写入文件

       ::get('public/1.txt');

       ::exists('public/1.txt');

       ::url('public/1.txt');

// 生成文件访问链接

asset('storage/1.txt');       
```

# 邮件

```bash
$ php artisan make:mail MailClass
```

在 `build` 方法中完成邮件的配置

```php
Mail::to()->send(new MailClass);

      ->queue(new QueueClass())
```

# 消息通知

```bash
$ php artisan make:notification NotificationClass
```

```php
class DemoClass
{
    use Notifiable;
}

$demoClass->notify(new NotificationClass());

Notification::send($users, new InvoicePaid($invoice));
```

# 事件

事件（Events） 监听器（Listeners）

例如一个 用户注册事件 可以对应 邮件 短信 等监听器

控制器中调用一个事件

event(new MyEvents());

将 事件 与 监听器 注册

`EventServiceProvider` $listeners=['事件'=>['监听器'，'监听器2']]

监听器接收 事件 示例 进行逻辑处理

监听器可以放入队列中
