---
title: Moment.js Depreciation warning
date: 2019-07-30 10:41:41
tags:
  - momentJS
categories:
  - NPM
---
## What is Moment.js?
官方文件：[Moment.js](https://momentjs.com)
可以用於時間的格式化、設定、轉換及運算等，可以省去使用大量的 Javascript 函式來處理．

## Problem
從資料庫取得的時間為 YYYY/MM/DD，但因為是 String，所以使用 moment.js 轉換
```javascript
const eDate = this.$moment(EndDate).format('YYYY/MM/DD') // EndDate為資料庫傳回的資料，值為 2016/12/12
console.log(eDate) // 2016/12/12
```
可以成功格式化時間，但會跳出 depreciation warning，warning內容如下：
![screenshot](warning.png)

## 解決方式
相同 issue: [Deprecation warning: value provided is not in a recognized RFC2822 or ISO format #156](https://github.com/adopted-ember-addons/ember-pikaday/issues/156)
原因：因為moment 目前可直接辨識x的時間僅 RFC2822 和 ISO 形式，但從資料庫傳回來的`EndDate`並非此兩種形式之一
**解決方式：告訴 moment 回傳的時間是什麼形式即可**

```javascript
const eDate = this.$moment(EndDate, 'YYYY/MM/DD').format('YYYY/MM/DD') 
console.log(eDate) // 2016/12/12
```