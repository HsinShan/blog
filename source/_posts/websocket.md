---
title: websocket
date: 2019-04-08 09:24:41
tags:
  - websocket
catogories:
  - websocket
---

**What is Websocket?**
為一種通訊協議，為**持續的**雙向連線，一旦透過 Javascript 建立連線就不斷線。

**Websocket v.s. HTTP**
Websocket 和 HTTP 傳遞不太相同，因為 HTTTP 要一個 request 一個 response，但 websocket 是一直 watch 資料庫，僅收跟發的動作，當**收**到資料庫有變動的資訊時，立即**發** response，所以並沒有 request 這個動作。
簡單來說， HTTP 只能由 client 端發送 request 才能取得 server 的 data，但 Websocket 可主動將 server 端的 data 發送給 client 端=> 適用在**需要立即偵測 data 變動**

**實作**

1. 建立 Websocket
   `var ws = new WebSocket(url, [protocol] );`
   url 為指定連接的 url(required)，protocol 則為可接收的通訊協議(optional)

2. Websocket 事件

```javascript
ws.onopen = function(e) {
  // 開啟 Websocket時，會觸發的事件
};

ws.onmessage = function(e) {
  // 接收 message 時，會觸發的事件
};

ws.onerror = function(evt) {
  // 連接時發生錯誤會觸發的事件
};

ws.onclose = function(evt) {
  // 關閉連接時會觸發的事件
};

// 可用 function
ws.send("Hello WebSockets!"); // 發送數據
ws.close(); // 關閉連接
```
