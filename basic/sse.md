---
title: HTML5 Server-Sent Events + PHP
date: 2018-05-26 13:00:00
updated:
comments: true
tags:
- PHP
- HTML
categories:
- PHP
---

本文介绍 `Server-Sent Events` 服务器发送事件 `SSE`。

HTML5 SSE 事件允许网页获得来自服务器的更新。

<!--more-->

```js
var source = new EventSource("demo_sse.php");

source.onmessage=function(event) // 当接收到消息
{
    document.getElementById("result").innerHTML += event.data + "<br>";
};

source.onopen(); // 当通往服务器的连接被打开

source.onerror(); // 当发生错误
```

```php
ini_set('max_execution_time', '0');

header('X-Accel-Buffering: no');
header('Content-Type: text/event-stream');
header('Cache-Control: no-cache');

while(1){
  // id event retry data \n\n
  echo "id: 1\nevent: my_event\nretry: 100\ndata: my_data \n\n";

  ob_flush();
  flush();

  sleep(1);
}
```

* `retry` 服务器端 N 秒内没有发送任何信息，则开始重连。

## More Information

* https://blog.csdn.net/kkgbn/article/details/53159791

* https://my.oschina.net/u/3095457/blog/1036952
