---
title: Vuetify v-select 及 v-dialog 在 IOS 不會在 blur 時關閉
date: 2019-08-23 14:14:01
tags:
  - directive
  - vue event
  - Virtual DOM
categories:
  - vue
  - vuetify
---
## Problem
Vuetify 的 v-select 及 v-dialog 在 IOS 的ＡＰＰ上，不會在 blur 時關閉，必須點擊外面兩下才會關閉，但在Android是可以的。

怪異的bug:
1.在點擊外面時，他本身的 blur event 有時候不會觸發
2.使用 IOS 的 chrome 開啟，第一次啟動開新視窗不會有此問題，但重整後就會有此問體

## 解決方式
**可能原因**：在 IOS 裝置上，必須用原生 IOS 寫法較不易出錯．且加上此專案由 cordova 生成 IOS app，所以可能才會出現此 bug
**解決方式**：
1.改為使用 IOS 常見的 select 方式 -> action sheet (MintUI 有)
2.建立 click-outside directive，判斷是否點擊到該元素之外的區域，如果點擊到外面則強制關閉
-> (我們使用的方式) 因專案已開發到一段落，為避免所有 select 都需更動其值及選項的寫法

``` javascript
Vue.directive('click-outside', {
  bind (el, binding, vNode) {
    const bubble = binding.modifiers.bubble
    const handler = (e) => {
      // 因為 v-select 及 v-dialog 的所有 event(e.g. click、focus、blur)都是屬於 vue event，所以必須獲取該vue component才有辦法呼叫到 vue event
      if (bubble || (!el.contains(e.target) && el !== e.target)) {
        // 為了獲取該 vue component，所以以該綁定的虛擬節點來取得，vNode.componentInstance即為該元素節點對應的組件實例
        if (vNode.componentInstance.$el.className === 'v-dialog__container') {
          // dialog 關閉的方式
          vNode.componentInstance.isOpen = false
        } else {
          // select 關閉的方式，此 blur event為 vue event
          vNode.componentInstance.blur()
        }
      }
    }
    // 給此 element 加上 private 變量，方便之後移除事件監聽時可以使用
    el.__vueClickOutside__ = handler

    // add Event Listeners
    document.addEventListener('click', handler)
  },
  unbind (el, binding) {
    document.removeEventListener('click', el.__vueClickOutside__)
    el.__vueClickOutside__ = null
  }
})
```
最後只需在遇到 v-select 及 v-dialog 時，綁定此 directive 即可
例如：

    <v-select v-click-outside :items="items" placeholder="請選擇"/>


directive 想法來源文章：[Vue 自定义指令实现点击元素外触发事件](https://segmentfault.com/a/1190000017166675)