---
title: Props Data Render
date: 2019-07-30 12:04:57
tags:
  - prop
categories:
  - vue
---

**Props 為 one-way-down binding**
Vue 的 props 並非雙向綁定，只有在 parent 更新 props 時，child 的 props 值才會跟著更新。為了防止 child 不小心更動 parent 的值，所以除了從 parent 更新 props，Vue 沒有提供其他更新方式

要特別注意的是，當 props是 Array 或 Object 時， props 是傳 reference 下來，所以在 child更動會導致 parent 的也被更動。