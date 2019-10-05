---
title: 什麼是 Event Loop?
date: 2019-10-05 12:41:00
tags:
  - event loop
  - blocking
categories:
  - Javascript
---

## What is Event Loop?

首先先看一下 MDN 怎麼說 -> [並行模型和事件循環](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/EventLoop)  
當中有提到 `queue.waitForMessage` 和 NeverBlocking 的特色  
簡單來說，Event loop(事件循環)是用於幫助 Javascript 的單線程運行不會 blocking，也就是**Javascript 處理異步的原理**

## What is Blocking(阻塞)

JS 為單線程(Single threshold)，所以程式碼會在堆疊(Stack)中被執行，一次只執行一個程式碼片段。
所以如果遇到像下面代碼的無窮迴圈呢？

```javascript
function foo() {
  return foo();
}
foo();
```

當遇到無窮迴圈時，堆疊會一直被疊加上去，然後當瀏覽器吃不消時，他就會丟出 Error!!
所以像是程式碼執行時一直在轉圈圈，沒有執行完的情況，就會被稱作 Blocking!! 也就是 Javascript 的主線程塞車了！

## Event Loop 的作用

#### Stack v.s. Queue

Javascript 在執行時主要分成**主線程**和**任務佇列**：  
1.主線程（Stack) -> LIFO  
2.任務佇列（Event queue) -> FIFO -> 放異步任務

#### MacroTask v.s. MicroTask

而任務佇列又有分 **MacroTask** 跟 **MicroTask**  
1.MacroTask: script 全部代码、setTimeout、setInterval、setImmediate、I/O、UI Rendering
2.MicroTask: Process.nextTick（Node 独有）、Promise、MutationObserver
注意： **Async/Await 算是 MicroTask**
因為 Async/Await 運作的時候，他會在底層轉換為 Promise，舉例來說：

```javascript
async function a() {
  await b;
  console.log("a() end");
}
```

此段程式碼其實就可以理解成以下程式碼

```javascript
async function a() {
  return RESOLVE(b).then(() => {
    console.log("a() end");
  });
}
```

**await 之後的程式碼會進入 MicroTask Queue**
也就是 b 會在主線程被執行，然後會推一個 Promise 進入 MicroTask Queue 中，當主線程執行完，要開始執行 MicroTask Queue 中的此 Promise 物件時，他會在執行完此 Promise 後，再把 then 的 callback 再推進 MicroTask Queue 中，需注意的是這個 then 的 callback 要重新排隊。

#### 運作方式

Event Loop 簡單來說就是**主線程（Stack）會不斷的從 Task Queue 中讀取事件**，也就是前面 MDN 中所提及的 `queue.waitForMessage`。
在 Stack 是空的時候，它就會去看 Task Queue 中有沒有任務，有的話就把第一個任務放到 Stack 當中執行。重要的是，他會優先去查看 MicroTask Queue，當 MicroTask Queue 都執行完了，才會去看 MacroTask Queue。所以常常 Event Loop 的實作方式都是如下面的程式碼：

```javascript
while (queue.waitForMessage()) {
  queue.processNextMessage();
}
```

Event Loop 常見面試題解析： [一次弄懂 Event Loop（彻底解决此类面试问题）](https://juejin.im/post/5c3d8956e51d4511dc72c200)
