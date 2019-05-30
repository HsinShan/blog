---
title: Web Storage v.s Cookies
date: 2019-04-13 16:57:41
tags:
  - cookies
  - localStorage
  - sessionStorage
catogories:
  - web storage
  - cookie
---

### What is Web Storage?

讓網頁可以將資料直接存在**本地**端，如同 Cookie 。但因為 Cookie 不宜存放太大量的資料，所以會使用 web storage。
種類有兩種: **sessionStorage** 和 **localStorage**

|          |           sessionStorage           |                             localStorage                              |
| -------- | :--------------------------------: | :-------------------------------------------------------------------: |
| 生命週期 | 生命週期非常短，該分頁關閉即被清除 | 只要沒有被清除(`removeItem()` 或 `clear()`)，會被永久保存在 client 端 |
| 作用域   |   該分頁(同一個視窗)，無法跨分頁   |           可以跨瀏覽器分頁(要同一個瀏覽器，但視窗可以不同)            |

---

### What is Cookie?

**用途 : 解決 http request 無狀態的問題，可將狀態保存於 Cookie 中**
`Cookies` 通常會由 server 端設置，但也可由 browser 端生成。若由 browser 端生成，browser 關閉，cookies 會被清除。另外，因為 Cookie 會保存在 request 的 header 中，所以容量有限制，僅能 4 KB，也**不宜保存太多數據**，否則會影響網頁的效能。
Cookie 通常用於記錄登陸訊息或購物車資訊。

詳細內容: [HTML5 Web Storage](https://www.huanlintalk.com/2012/06/html5-web-storage.html)

<style scoped>
th{
  width:40%; 
}
th:first-child{
  width:20%;
}
</style>
