---
title: HTML5 實用 tags
date: 2018-09-08 13:27:19
tags:
  - HTML5
  - Semantic tag
categories:
  - HTML5
---

### Semantic tag

詳細內容: [如何理解 HTML 結構的語意化](https://www.itread01.com/content/1547075523.html)

HTML5 新增了很多語意化的標籤，在實作上非常實用。
**可強化結構，避免語意不明的 tag 不斷出現**
e.g `<header>`,`<nav>`,`<footer>`可以取代 `<div>`

### Input Types

`<input>`的 `type` 新增很多種，e.g. email, tel, radio, date, number...
只要設定好 type，就會自動進行表單驗證，不需要自己寫驗證規則。
而且像是 `<input type="tel">`，在輸入時會自動跳出數字鍵盤。

### 表單驗證

只要加上 `required`就代表必填，例如:`<input type="tel" required>`
