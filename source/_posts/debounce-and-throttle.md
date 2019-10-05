---
title: 淺談 Debounce 和 Throttle - 關於 DOM 的效能優化
date: 2019-08-29 11:15:51
tags:
  - closure
  - debounce
  - throttle
categories:
  - Javascript
---

## 前情提要

簡單來紀錄一下為何會接觸到 debounce 和 throttle，原因是因為接到一個任務，要在 scroll 時，更改 toolbar 的高度，因而在 search 時，發現了 debounce 和 throttle !!

## Why use Debounce and Throttle?

**目的：防止函數被高頻調用**
相信在某些功能的實作上，我們會需要 mouseMove, scroll, resize 這些事件，這些 event 發生就會為觸發他們的 callback。但他們往往會被頻繁觸發，加上 callback 中常有綁定一些 DOM 節點的操作，因此這些操作會觸發 DOM 重新計算，一旦頻繁觸發，會大大消耗整體效能。
可先參考此篇文章 -> [網頁 DOM 事件的效能優化：Debounce 和 Throttle](https://mropengate.blogspot.com/2017/12/dom-debounce-throttle.html)

## What are Debounce and Throttle?

#### Debounce(去抖動)

強制要求在停下連續操作之後，等過指定時間（通常為極短的微秒），再觸發該動作的 callback。也就像是將指定時間（自行設定的毫秒）內的觸發合併成一個，在指定時間的開始(設定 immediate = true)或結束一起觸發。
**非常適合用於 input 時，可在停止輸入後，在一併發送 request，或是停止輸入再進行 validation**

```javascript
/**
 *
 * @param func {Function}   實際要執行的函数(該動作觸發的回調函數)
 * @param delay {Number}  延遲的時間，單位是毫秒
 *
 */
// 若再次觸發的時間小於 delay，timer就會重置，從新開始計時器
function debounce(func, delay) {
  var timer = null;
  // 為 closure，才能防止 timer 正常重置
  return function() {
    // 先將觸發事件的上下文及參數存下，以傳遞給 callback
    var context = this;
    var args = arguments;
    clearTimeout(timer);
    timer = setTimeout(function() {
      func.apply(context, args);
    }, delay);
  };
}
```

#### Throttle(函數節流)

將 callback 的執行時間固定，以確保在該執行期間內，callback 不會再被調用

```javascript
/**
 *
 * @param func {Function}   實際要執行的函数(該動作觸發的回調函數)
 * @param threshold {Number}  回調函數執行的時間，單位是毫秒
 *
 */
function throttle(func, threshold) {
  var last; // 記錄上次執行的時間
  var timer;

  threshold || (threshold = 250);

  // 每過 threshold 毫秒就執行一次 func (callback)
  return function() {
    // 先將觸發事件的上下文及參數存下，以傳遞給 callback
    var context = this;
    var args = arguments;
    var now = +new Date();

    if (last && now < last + threshold) {
      clearTimeout(timer);
      timer = setTimeout(function() {
        last = now;
        fn.apply(context, args);
      }, threshold);
    } else {
      last = now;
      fn.apply(context, args);
    }
  };
}
```

參考文章：

1. [Debounce 和 Throttle 的原理及实现](http://hackll.com/2015/11/19/debounce-and-throttle/)
2. [理解 Debouncing 与 Throttling 的区别](https://www.jianshu.com/p/e91775195608)
