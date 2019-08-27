---
title: Directive
date: 2019-08-21 12:22:47
tags:
  - directive
categories:
	- vue
---
## What is Custom Directive?
也就是客製化指令，vue 本來就有`v-model`、`v-show`這些指令，但有時候我們必須對 DOM 進行一些底層操作，或直接取得底層 DOM 的某些 element，但因為 MVVM 讓 vue 的 view 和 viewModel 完全分離，所以操作 DOM物 件不應該放在 view 中，因此 vue 提供客製化指令，也就是使用 directive。
官方文件：[Custom Directive](https://vuejs.org/v2/guide/custom-directive.html)

## 使用方式
``` javascript
// Register a global custom directive called `v-focus`
Vue.directive('focus', {
  // 第一次連到該綁定的元素時使用，適用於需要一次性初始化設定時
  bind: function (el, binding, vnode) {
    console.log(el) // 綁定的DOM元素，方便我們直接操作DOM物件
    console.log(binding.value) // bind 的東西
    console.log(vnode) // 綁定的虛擬節點
  },
  // 適用於當綁定元素被插入DOM時
  inserted: function (el) {
    // Focus the element
    el.focus()
  },
  // 當綁定的虛擬節點更新時會呼叫，但有時候會在更新之前就呼叫
  update: function (el) { 
  },
  // 綁定元素所在的 component 更新時使用
  componentUpdated: function (el) {
  },
  // 用於解除綁定時
  unbind: function (el) {
  },
})
```
**Directive Hook Arguments**
請參考官方文件：[Directive Hook Arguments](https://vuejs.org/v2/guide/custom-directive.html#Directive-Hook-Arguments)