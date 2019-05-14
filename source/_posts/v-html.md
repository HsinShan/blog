---
title: v-html
tags:
  - vue-tutorial
  - XSS
url: 246.html
id: 246
categories:
  - vue
date: 2019-05-03 06:53:03
---

較不推薦使用，因易受 XSS 攻擊，因為可以加入 html 代碼帶入 DOM 中，代表也可以使用 `<script></script>`，這樣網站易被注入惡意程式，竄改原先要顯示的內容。 因 JS 可定義 browser 的動作，所以當外來注入 JS 指令，對於網站安全非常不利。

**What is XSS?** Cross-Site Scripting(跨網站指令碼攻擊)，像是可透過 POST 時，將惡意指令植入要傳遞的參數，就可以攻擊 server。
種類:
1.Stored XSS (儲存型):當有使用者輸入的動作，像是有留言板或是論壇的網頁，若沒有將特定代碼轉換，則可透過輸入 script 標籤(因會自動編譯成 HTML)，植入任意程式來攻擊 server。
2.Reflected XSS (反射型):不會更動 server 中資料的內容，僅透過 GET request 時，更改 URL 中?後面的參數，在其中加入 `<script></script>`，即可透過 JS 攻擊 server
3.DOM-Based XSS (基於 DOM 的類型):只能親自去要攻擊的電腦，打開該網頁。因為 DOM 的呈現和 server 無關，僅 browser 的渲染。

解決方式: 1.轉換特殊標籤字元，像是遇到 script 標籤就轉換成別的字元 2.白名單機制:限制 input 的內容
