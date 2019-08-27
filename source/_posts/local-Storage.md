---
title: Hybrid App 將資料存在 local 端
date: 2019-07-31 17:10:41
tags:
  - localStorage
  - SQLite
catogories:
  - hybrid app
---
## Why save data on device?
有些時候當希望減少 api 請求次數，可以避免來回頁面需重複 request 頁面所需要的 data，或希望登入後 device 可以自動存取一些資訊，以利於下次開啟 app 時，不需要再次登入也可以看到這些資訊，或是記住帳號密碼等功能，就會需要將這些資料存在 local端。

如果是網頁的話，我們可以將這些資料存在 cookie 或 webStorage，{%post_link web-storage%} 有詳細的比較。但如果是 Hybrid APP 呢？

## Hybrid App 存資料在 local 的方式
1. localStorage :較為簡單快速
限制： 他的 key 只能存 String，所以可以先將 JSON 變 String 再存進去
可能發生的問題：localStorage 最大容量為５MB ，不論在 Android 或 IOS，都有可能因為內存不足而被清除
2. 在 local 端放一個 DB -> SQLite 數據庫
3. [PonchDB](https://pouchdb.com/)：為開源的 JS database

## 注意：存密碼在 local 端的弊病
雖然通常在本地端存密碼資訊，大多都會進行加密(encryption)的動作，但因為加密是可以被逆行，所以還是不安全！！
#### hash v.s encryption
hash 是不可逆的，但 encryption 可藉由雙向加解密取得原本密碼

#### 處理方式
可以加上 token (例如 JWT/Json Web Token) 來對密碼進行加密，但是還是不保證安全！！
最安全的做法就是自己記密碼！

相關文章：[Hybrid App Developers: Don’t Store Your User’s Passwords](https://www.joshmorony.com/hybrid-app-developers-dont-store-your-users-passwords/)

