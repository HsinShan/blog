---
title: SPA
date: 2019-04-21 10:10:41
tags:
  - SPA
  - memory leak
categories:
  - Frontend
---

## Single Page Application（SPA）

只有一個 index.html 檔案，全部的動作只在 index 這個頁面上實現。只跟 json 溝通，透過 javascript 來切換 router，所以頁面不會重載，切換速度非常快。
**優點**  
1.降低伺服器的負擔  
2.加強使用者體驗，因為網頁載入速度非常快
**缺點**  
1.memory leak 問題: 因為 SPA 切換頁面不會重載，所以若未處理內存，會導致內存不斷提高，造成 browser 變慢或 crash 的情況  
2.狀態管理問題，因頁面切換快速，若 user 快速點擊，會有 response 來不及拿到的問題，而造成資料顯示錯誤  
3.不利於 SEO， 因為 index 檔解析下來往往沒什麼內容  
4.需要一次載下大量的 JS 包，或其他頁面的 template
