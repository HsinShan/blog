---
title: 實現多個 button 點擊效果--作用域
date: 2018-07-23 10:36:59
tags:
  - scope
  - list
  - this
categories:
  - Javascript
---

## 功能: 多個按鈕點擊 alert 該按鈕對應的 index

錯誤寫法:

```javascript
// 假設共有 5 個 button
for (var i = 0; i < btnList.length; i++) {
  btnList[i].onclick = function() {
    alert(i); //不管點哪個 button 都是 alert 5
  };
}
```

## Why alert 5??

=> 先後順序問題，因為先跑完 for 迴圈，才有點擊事件
(2019/10/05 更新)
因為 for 是主線程，然而 click 事件會被放到任務佇列中，等主線程跑完才會跑任務佇列，所以他會等 for 跑完，i 這時候就會變成５。

**預解析**
1 `var i;`

**逐行解析**
i=0 => `btnList[0].onclick = function() {alert(i);}`
i++ // i=1
i=1 => `btnList[1].onclick = function() {alert(i);}`
i++ // i=2
i=2 => `btnList[2].onclick = function() {alert(i);}`
i++ // i=3
i=3 => `btnList[3].onclick = function() {alert(i);}`
i++ // i=4
i=4 => `btnList[4].onclick = function() {alert(i);}`
i++ // i=5
**退出迴圈，此時 i=5 ，但因為尚未有點擊事件，所以當點擊發生時，只會 alert 5**

## 正確寫法

1.把所有 button 放入 array 中，搭配 this

```javascript
// 假設共有 5 個 button
for (var i = 0; i < btnList.length; i++) {
  btnList[i].onclick = function() {
    alert(this);
  };
}
```

用 this 就能抓到當前被點擊的 button(this 誰調用他就指向誰)

2.使用**立即函式(IIFE)** (2019/10/05 更新)

```javascript
// 假設共有 5 個 button
for (var i = 0; i < btnList.length; i++) {
  btnList[i].onclick = function() {
    (function(j) {
      alert(j);
    })(i);
  };
}
```
