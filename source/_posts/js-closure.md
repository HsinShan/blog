---
title: Closure
date: 2019-03-29 09:36:41
tags:
  - closure
  - scope
  - lexical scope
categories:
  - Javascript
---

### What is Closure?

**function + 建立該 function 的環境(此環境是任意的局部變數，像是 function)**

```javascript
// closure
function test() {
  var str = "Hello World";
  return function() {
    alert(str);
  };
}
var y = test();
y();
```

特點:

1. 可以建立類似物件導向的 private 變數，避免 global 變數發生重複更改而導致值的錯誤
2. 資料隔離的效果

```javascript
function counter() {
  let count = 0; //private variable
  function add() {
    count++;
  }
  return add();
}
var countDog = counter();
countDog(); // 1
countDog(); // 2

var countCat = counter();
countCat(); // 1
countCat(); // 2
```
