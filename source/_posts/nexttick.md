---
title: nexttick
date: 2019-04-12 10:40:22
tags:
  - nexttick
  - vue-tutorial
categories:
  - vue
---

**What is nexttick?**
**nexttick 也就是等到下一個 tick 再執行的意思**

Javascript 是 **single threshold(單線程)**，也就是一次只能做一件事情(執行一行 code)。(Java 是多線程，可以一次執行多行 code)
所以雖然說 Vue 是即時更新 DOM，但其實是**異步執行更新 DOM**，所以實際上還是得等到整個 tick 跑完(也就是此次的主 t
ick 加上任務 tick 都跑完)才會更新，進入下一次主 tick。所以若想要取得更新後的 DOM data，就需要使用 nexttick。

**執行流程**：
主 tick(同步代碼)執行 => 查找任務 tick(異步隊列)並推入執行線 => 執行 Vue.nextTick(因進入下一次主 tick)
※任務 tick(異步隊列)也屬於一個單獨的 Tick，不會和主 tick 同時發生。 **回調函式就是屬於異步**

**適用時機**

1. 適用於需要操作 DOM 更新後的 element
2. `created()` 若需要操作 DOM 上 element 的值，也需要使用 nexttick，因為在 created 時， DOM 尚未被渲染

詳細內容: [JavaScript 運行機制講解：再談 Event Loop](http://www.ruanyifeng.com/blog/2014/10/event-loop.html)

```javascript
vm.message = "changed"; //數據改變

console.log(vm.$el.textContent); // DOM還沒更新，並不會得到'changed'

Vue.nextTick(function() {
  console.log(vm.$el.textContent); //可以得到'changed'，因為 DOM 更新了
});
```
