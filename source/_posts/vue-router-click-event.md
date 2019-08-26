---
title: router-link 導致 @click 失效
date: 2019-08-01 16:32:23
tags:
  - vue router
  - vue event
categories:
	- vue
---
## Problem
在 `router-link` 中，click event 會無法運作
``` Javascript
<router-link ＠click="goNext" to="/">Home</router-link>
// 並沒有進入 goNext 這個 method
```
問題 issue : [Router-Link doesn't support v-on:click #800](https://github.com/vuejs/vue-router/issues/800)

## 解決方式
原因：因為 vue router 點擊時，預設會觸發他的 vue event，所以並沒有觸發 browser event (native 的 event)
解決方式：使用 `@click.native`，將點擊觸發的事件改成 native 的 event

## vue event
vue 的 event 是**使用 emit方式建立的**，和原生的 event是不一樣的
