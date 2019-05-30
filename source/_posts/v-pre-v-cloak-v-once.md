---
title: v-pre & v-cloak & v-once
tags:
  - vue-tutorial
url: 238.html
id: 238
categories:
  - vue
date: 2019-05-02 09:17:53
---

**v-pre**: 跳過其包裹的屬性的編譯過程(即不編譯它)

```html
<span v-pre> {{message}} </span> <span> {{message}} </span>
```

Output:
1 `message`→ 因為沒有被編譯
2 message 所存的值 使用 v-pre 可跳過每有指令的節點，加快編譯

---

**v-cloak**: 解決 vue instance 完成編譯前顯示的問題 通常會在 CSS 中加上

```Css
[v-cloak]{
  display:none;
}
```

以確保在編譯後才會看到此指令包裹的元素

---

**v-once**: 只 render 該元素一次，隨後會被視為靜態內容而跳過，不會再次 render 他 可用在要優化「更新」性能時(因為可以跳過不必要的更新) 在 Vue 底層實現上，Vue 會將 template 編譯成 Virtual DOM 的 Render 函數 然後能自己計算最少須重新 render 多少組件 並把 DOM 操作次數減到最少。
Vue 的 Data-Binding 最常見的形式 →**Mustache**(雙大括號) 其綁定的數據對象，值一旦發生改變，插值處 DOM 內容都會更新。 → 可以透過 v-once 執行一次性插值，使其內容不會隨值改變而更新。
