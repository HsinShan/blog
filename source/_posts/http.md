---
title: HTTP
tags:
  - Cache
  - HTTP
url: 252.html
id: 252
categories:
  - 計算機概論
date: 2019-05-05 03:49:18
---

## What is Http?

HyperText Transfer Protocol 獲取網路資源的通訊協議 為一種 client-server 協議，由 client 端發起 request，由傳輸層中的 TCP 協議建立連接，及各種 Proxy(代理)轉發，最後 server 端回傳 response。 Proxy(代理)像是緩存、過濾、歷史紀錄等。

**URI v.s. URL** URI=URL+URN(uniform resource name:類似於表示此 url 的身分)

## HTTP 的性質:

1.  持久連接:早期 HTTP 在建立連接後都會斷開連接，等下次 request 再重新連接，但當 request 次數提高，或 data 越來越龐大時，重複連接會造成速度變慢。因此後來 HTTP 改為持久連接，穰兩端若沒有提出段開連接的請求，就一直保持連接，以便下次 request 時可以復用該連接，避免重複載入的 loading，也加入頁面載入的速度。 另外，因 request 是有先後順序，得讓前面的 request 收到 response 後，才會執行下一個 request。因此有管道化的方式，可一次發送多個 response，然後 server 在一個一個 response。
2.  無狀態:每個 request 都是獨立的，即使在同一條連接上，request 之間也沒有關係。但當需要狀態管理時(像是須保存有登錄的狀態時)，就需引入 Cookie 技術，將每個 request 和 response 都加上 cookie 信息，即可保存狀態。

## 緩存(Cache) : 2019/09/30 新增詳細文章 {%post_link http-cache%}

由 HTTP 控制，可以自動將資源副本保存在 local 端，減少 client-server 端的通信次數，不但可以加速頁面載入，也可以減少網路延遲。
在 client 端的緩存中搜索指定資源的副本 → 有副本:進行新鮮度檢測(就是看文檔有沒有過期) → 不新鮮:和 server 進行再驗證，驗證通過舊更新資源新鮮度，在將最新資源的副本放入緩存中
※no-cache:向 server 進行新鮮度驗證才能進行緩存 no-store:禁止緩存
