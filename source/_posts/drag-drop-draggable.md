---
title: vue-drag-drop 的 draggable 並無正常運作
date: 2019-05-23 10:05:29
tags:
  - vue-drag-drop
categories:
  - NPM
---

npm package : [vue-drag-drop](https://www.npmjs.com/package/vue-drag-drop)

有提供 property: draggable 來控制可不可以拖曳，但儘管設定 `:draggable=false`，也只有點第一下時被禁止拖曳，之後還是會被拖曳。

原因: **CSS rule 中的 user-select**
一般 OS 　初始設定都可以 text-selection，所以會被允許拖曳 text。

解決方式: **更改 user-select 設定，將 text-selection disabled**

```CSS
element{
    -webkit-touch-callout: none; /* iOS Safari */
    -webkit-user-select: none; /* Safari */
     -khtml-user-select: none; /* Konqueror HTML */
       -moz-user-select: none; /* Firefox */
        -ms-user-select: none; /* Internet Explorer/Edge */
            user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome and Opera */
}
```
