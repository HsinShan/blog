---
title: JS 特殊 type
date: 2018-07-17 15:56:49
tags:
  - type
categories:
  - Javascript
---

## 動態決定變量型別

Javascript 不須指定變量的 type， 他會自己動態決定。
用 `typeof element` => 取得 element 的 type

## 特殊 type

1.undefined: 為**已定義但未初始化**或**未定義**(會跑 error)  
 所以一定都要初始化，盡量不要有 undefined type  
2.null: 有初始化，但值為空 => **type = Object**  
 ※注意: null == undefined 是成立的  
3.NaN(Not a Number): 非數值，但 **type 仍然是 number**

e.g.

```javascript
var n5 = 0 / 0; // return NaN
var n6 = 12 / 0; // return infinity
```

如果 0/0 沒有返回值(即 n5 沒有值)，之後用到 n5 程序會報錯
※ NaN != NaN (NaN 是不等於任何值的)，所以若要判斷是否為 NaN，要用 `isNaN(n5)`
