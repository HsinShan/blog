---
title: 有關 HTML5 新增的 script 屬性
date: 2019-09-30 11:35:30
tags:
  - HTML5
  - Script
categories:
  - HTML5
---

## 新增 script 屬性： async & defer

```javascript
<script src="/new.js"></script>
```

**預設用法**，下載後會先執行這個 js 檔案，再繼續繪製頁面

```javascript
<script async src="/new.js"></script>
```

**非同步**執行，一定要搭配 src 屬性，下載後會執行此 js．但同時也會繼續繪製頁面及執行其他 js
**使用時機**：此 js 和其他的 js 無連帶關係，即不需等待其他的 js 執行完，可獨立作業。

```javascript
<script defer src="/new.js"></script>
```

一定要搭配 src 屬性，整個頁面繪製完及分析完才會執行此 js，**類似把它放在頁尾的情況**

```javascript
<script async defer src="/new.js"></script>
```

一定要搭配 src 屬性，要整個頁面都下載及分析完成後才會**非同步**執行這個 js 後面剩下的部分。
