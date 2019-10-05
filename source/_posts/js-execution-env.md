---
title: Execution Context
date: 2018-07-23 10:18:39
tags:
  - execution context
  - scope
categories:
  - Javascript
---

### What is Execution Context?

Execution Context 即為 js 的「執行環境」。主要分為 3 種執行環境:

1. Global: 一個 js 檔，只有一個 global context
2. function: 一個 function 會建立一個執行環境，call function 也會建立一個新的執行環境
3. eval()

### Execution Context 堆疊

當進入新的執行環境，會先處理新的執行環境 -> **執行堆疊(stack)**的概念，所以是 LIFO (Last In, First Out)

```javascript
// Global context
var a = 1;

function count() {
  // function context
  var b = 2;
  var c = 3;

  function countb() {
    // another function context
    b++;
    return b;
  }
}
```

進入 js 檔 → 進入 `Global context` → 進入 `count() function context` → 進入 `countb() function context`
→ `countb() function context` 執行結束 → `count() function context` 執行結束 → `global context` 執行結束

詳細內容: [理解 Javascript 執行環境](https://andyyou.github.io/2015/04/18/what-is-the-execution-context-in-javascript/)
