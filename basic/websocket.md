---
title: Websocket
date: 2018-05-25 13:00:00
updated:
comments: true
tags:
- PHP
- HTML
categories:
- PHP
---

`WebSocket` 是一种在单个 TCP 连接上进行全双工通讯的协议。

<!--more-->

```js
var ws = new WebSocket(url, [protocol] );

var ws = new WebSocket("ws://example.com", [protocol] );

ws.onopen = function (){
    ws.send('message');
}

ws.onmessage = function (evt){
  var received = evt.data;
}

ws.onclose = function (){

}
```
