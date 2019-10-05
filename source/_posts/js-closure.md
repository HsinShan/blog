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

## Why Closure? (2019/09/23 更新修正)

1.用於**保存變數**，避免變數因為沒有被參照（refer) 而釋放記憶體  
2.可建立私有方法(待補充)  
3.可建立函式工廠(待補充)

<!-- TODO: 更新 -->

```javascript
function counter() {
  let count = 0; //private variable
  return function add() {
    return count++;
  };
}
var countDog = counter();
// 建立一個專門屬狗有幾隻的 counter(獨立的執行環境）
// function 中的 count 變數物專屬於狗的數量
countDog(); // 1
countDog(); // 2

var countCat = counter();
// 建立一個專門屬貓有幾隻的 counter(獨立的執行環境）
// function 中的 count 變數物專屬於貓的數量
countCat(); // 1
countCat(); // 2
```
