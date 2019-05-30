---
title: Lifecycle
tags:
  - vue-tutorial
  - lifecycle
  - memory leak
url: 225.html
id: 225
categories:
  - vue
date: 2019-05-01 10:06:08
---

Vue 會將 data 跟 template 綁在一起，因此只需要定義好 data 的位置及內容 vue template 掛載順序(先 → 後) :子組件 → 父組件 → Vue instance

**beforeCreate**: 組件實體(vue instance)剛被建立(即`new Vue()`),綁在 HTML 上的屬性(attribute)被計算前。
**created**: vue instance 已建立,attribute 已綁定,但 DOM 還沒生成。 也就是說資料在 created 後才存取的到(別把資料初始化跟 ajax 寫在 beforeCreate，否則在 created 時抓到的資料會被洗掉)

---

**beforeMount**:模板 (template) 編譯或掛載至 HTML 之前
**mounted**:模板 (template) 編譯或掛載至 HTML 之後，DOM 渲染完畢

---

**beforeUpdate**:組件被更新之前
**updated**:組件被更新之後

---

**activated**:keep-alive 用,組件被啟動時呼叫
**deactivated**:keep-alive 用,組件被移除時呼叫 `<keep-alive></keep-alive>` 將其所包裹的組件狀態緩存，所以當填表單有上一步或下一步時，可用於保存已填好的資料。 所以當 `<keep-alive></keep-alive>` 的組件被移除時，可用 deactivated 來進行清理內存或改變數據

---

**beforeDestroy**:組件被銷毀前呼叫
**destroyed**:組件被銷毀後呼叫 component 銷毀方式: `vue.$destroy();`
目的: Avoid Memory Leaks(內存洩漏) 因為 SPA 不會重複刷新頁面，所以 JS 應用需要自行清理組件確保垃圾回收是以預期的方式進行。
Memory Leaks 當系統內存以等差級數增加時，到達某個極端點會造成該網頁 crash。 若是剛好在 server 用 browser 開啟該網頁，當內存過多造成 crash 時，也會使 server 因此掛掉。
e.g. `v-if` 指令可以控制是否顯示在 DOM 在上面，不顯示則在 DOM 上是完全沒有此物件，但在 Memory 中並不會即時清理，所以在每次狀態改變時(即隱藏或顯示)，memory 會增加，因為並未被回收。 因此適當的銷毀可以保持小內存的開銷。
