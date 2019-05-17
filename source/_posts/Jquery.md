---
title: Jquery
tags:
  - Juery
  - library
  - framework
url: 263.html
id: 263
categories:
  - Frontend
date: 2019-05-17 10:41:41
---

jQuery 為 Javascript 的 library，主要目的是為了**解決瀏覽器上的差異**，會不斷地隨著瀏覽器進化
特性:

1. 透過選擇器(selector)`$` 可以更方便選取和操作 DOM 對象
2. 數據和 view 是綁在一起的，若要改變 DOM 的值，必須先選取該 DOM 對象才能操作
3. 提供 `animate()` function，讓動畫流暢

缺點:

1. 在需要大量計算時(很多 Jquery 在跑)，效能較慢
2. 程式沒有有效率且規則的管理，會很長(所以現在前端流行用組件來管好自己內部的東西就好)

### library v.s framework

兩者皆是為解決某些問題而寫的 code，可避免重複寫相同的 code。
**library**: 提供一包已定義好的 class，掌控權在 user 手上，user 可自行調用自己想用的 function
**framwork**: 提供一個大框架，不僅是定義好的 class，連整個運作流程都已事先定義。掌控權屬於該框架， user 須將自己的 code 放入該框架中。
