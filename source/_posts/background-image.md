---
title: 讓 div 高度自適應背景圖片高度
date: 2019-03-15 15:22:56
tags:
  - background-image
categories:
  - CSS
---

#### 如何讓 div 高度自適應背景圖片高度?

=> 透過 padding 來設定

```css
div {
  width: 100%;
  background: url("../../assets/map/M-building.jpg");
  background-size: contain;
  background-repeat: no-repeat;
  width: 100%;
  height: 0;
  padding-top: 66.64%; /* (img-height / img-width * container-width) */
}
```

如果 container 寬度為 100% 就不需要乘 container-width
