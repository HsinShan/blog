---
title: Vue Router 的 scrollBehavior
date: 2019-08-14 18:03:12
tags:
  - vue router
  - scroll behavior
categories:
	- vue
---
## What is scrollBehavior of Vue Router?
當我們希望可以在切換到下一個 router時，希望下個 router 重新滾動到最上方，或者希望下一個 router 可以停留在現在滾動到的位置，就可以使用 Vue Router 提供的scrollBehavior。(例如要從列表頁面跳到編輯頁面，若希望在進入編輯頁面後，可以停留在列表看到要編輯的選項位置，就可以使用scrollBehavior)
官方文件：[Scroll Behavior](https://router.vuejs.org/guide/advanced/scroll-behavior.html#async-scrolling)
**但此功能只在 vue router 的 mode 為 html5 history 時適用。**

## 使用方式
``` javascript
const router = new VueRouter({
  routes: [...],
  scrollBehavior (to, from, savedPosition) {
    if (savedPosition) {
      return savedPosition
    } else {
      return { x: 0, y: 0 }
    }
  }
})
```