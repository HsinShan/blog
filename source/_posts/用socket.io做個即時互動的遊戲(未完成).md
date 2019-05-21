---
title: 用socket.io做個即時互動的遊戲(未完成)
tags:
  - socket
url: 249.html
id: 249
categories:
  - Boss_Coding
tags:
  - socket
date: 2019-05-04 04:02:31
---

老闆，來點寇汀吧:[https://www.youtube.com/watch?v=QVZcMx3jtG8&t=41s](https://www.youtube.com/watch?v=QVZcMx3jtG8&t=41s)

Socket.io:可用於即時互動的使用者介面，將 server 中的資料，在每個使用者的介面上做最即時的同步 e.g. Agar.io

**What is socket?**
socket 是通訊協定(電腦間對話的管道)，在電腦間建立通訊的管道

> A (電腦)====== B(Server)

傳統是先建立連線 中心 server 存在，負責保存所有狀態 其他終端電腦會傳給 server 訊息及狀態給 server 確認及審核 Server 負責傳遞訊息給所有電腦，及更新狀態(類似廣播的概念，但多是一對一的連結，所有人都不會再同一個頻道，需透過 server 傳遞) 同為通訊協議: MQTT 物聯網專用的通訊協定，類似全域廣播，有一個所有人都可以共用的頻道 OSC 常用於合成樂器的電動通訊協議

**頻道概念**:

A ===== B
頻道
/user: login user infomation
/game: attack(23)  defence(24)

//玩家 `A.emit("attack",{me:user,target:23}))`
//server

```javascript
B.on("attack", function(obj) {
  //通知所有人
  All.emit("bloodUpdate", { id: 23, blood: 30 });
});
```

類似 event bus 的概念，需透過訊息通道，制定各種要用的通道制定訊息，通常訊息是純文字

**優點**:

1. 簡化溝通，不需自行處理如何傳遞資料，只需透過 emit 跟 on 執行對應的 function
2. 非常及時同步
3. 可以在執行階段保存資料，server 端保存狀態，他會在 server 端保存 js 變數
