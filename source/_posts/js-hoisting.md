---
title: Hoisting
date: 2019-10-02 11:48:29
tags:
  - hoisting
  - ES6
categories:
  - Javascript
---

## 前情提要

最近在上六角學院[Javascript 核心篇](https://www.hexschool.com/courses/js-core.html)，對於 Javascript 的觀念可以說是大大的被翻轉。在這門課當中，我也有學到了 hoisting 的概念，但在面試的時候還是被問倒了...我才發現原來 hoisting 還有很多東西是我不知道的，所以就決定好好的研究一下!!
另外，我蠻推薦[我知道你懂 hoisting，可是你了解到多深？](https://blog.techbridge.cc/2018/11/10/javascript-hoisting/)這篇文章的，看完真的會對於 hoisting 有更不一樣的體悟！

## What is Hoisting?

簡單來說，就是在變數被宣告之前使用該變數，變數的宣告會被提升到上面去。
每個變數在宣告時都會經歷兩個階段：**創造階段**和**執行階段**  
舉例來說：

```javascript
var i = 1;
```

這行代碼其實在 javascript 會被分成兩個階段
-> 在創造階段會先宣告，叫記憶體保留空間給 i : `var i`
-> 在執行階段才會賦值，給 i 賦予 1 這個值 : `i = 1`

而當我們在變數宣吿前使用它時，就會發生 hoisting!!

```javascript
console.log(a); // undefined
var a = 1;
```

其實上面的代碼實際運作其來的順序是

```javascript
var a; // a 的宣告被提升了
console.log(a); // undefined
a = 1;
```

重要的是函式的 hoisting 會同時完成創造階段跟執行階段，也就是函式的值也會被賦予上去，也就是讓我們可以不須先宣告函式才能使用，這樣才能讓函式彼此互相呼叫。

```javascript
console.log(a); // function a(){alert('a')}
function a() {
  alert("a");
}
```

## ES6 新增的 let 跟 const 有 hoisting 嗎？

先看下面範例，看似 let 並無提升的行為

```javascript
console.log(a); // ReferenceError: a is not defined
let a;
```

但是!!!其實是有的!!請看下面範例：

```javascript
var a = 10;
function test() {
  console.log(a); // ReferenceError: a is not defined
  let a;
}
test();
```

照理來說，若 let 沒有 hoisting，a 應該會向上查找所以回傳 10，但這邊 a 並沒有回傳 10 反而回傳 **ReferenceError: a is not defined**
代表：`let a` 有被提升，但**提升後的行為和 var 不同**！！！

## Temporal Dead Zone：let 和 const 「提升之後」和「賦值之前」

let 和 const 和 var 的不同在於**提升之後 let 和 const 的宣告並不會被初始化為 undefined**，所以如果再宣告之前使用它是會拋出 Error。
