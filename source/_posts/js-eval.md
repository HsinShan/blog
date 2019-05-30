---
title: eval()
date: 2019-05-30 13:20:23
tags:
  - execution context
  - scope
  - eval
  - lexical scope
categories:
  - Javascript
---

### function eval(string)

`eval` 也就是 evaluate，會將其括號中的字串當作指令執行，括號中若無值會返回 undefined。

```javascript
eval("a=10");
console.log(a); // 10

eval("function fn1() { alert('Hello World!'); }");
fn1(); // alert('Hello World!');
```

1. 被 `eval()`執行的指令，其 {%post_link js-execution-env%} 等同 `eval()` 的執行環境。也就是說，當 `eval()` 在全局被調用時，`eval("a=10")` 所執行的 a 變數會是全域變數。
   因此，`eval()`也可以透過 `window.eval()`，將函式中的 private 變數，變成全域變數。

```javascript
function fn() {
  var str = 'function test(){console.log("Hello World!");}';
  window.eval(str);
}
fn();
alert(test()); // global 仍可以調用到 test()，因 test() 的執行環境在 gloabal
```

2. 非常適用於訂單處理，因為欄位名會隨著筆數增加而增加，所以若需要執行計算時，使用 `eval()` 搭配 for loop 可以使程式碼精簡

詳細內容參考:[JavaScript 的 eval() 用法介紹](http://icodding.blogspot.com/2015/12/javascript-eval.html)

### 避免使用 eval

1. 和 {%post_link v-html%} 相同，因括號中可以任意填入代碼，易受 XSS 攻擊
2. 會導致效能不佳: 因為 JS 會再編譯的時候進行最佳化，但 `eval()`會使 JS 在編譯時還無法取得其括號中的內容，所以不知道是否會改變原本的 Lexical Scope(語意範疇)，會導致 JS 引擎可能不進行最佳化，因而使網頁效能變差。

詳細資訊:[你懂 JavaScript 嗎？#11 語彙範疇（Lexical Scope）
](https://cythilya.github.io/2018/10/18/lexical-scope/)
