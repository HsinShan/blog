---
title: prop 的命名規則
date: 2019-04-11 10:17:41
tags:
  - prop
categories:
  - vue
---

父組件 =(data) => 子組件
使用 prop 將 data 從父組件傳遞到子組件

父組件

```html
<div id="app">
  <child-component :user-name="name"></<child-component>
</div>
```

子組件

```javascript
export default {
  props: ["user-name"]
};
```

因為 HTML 並不會區分大小寫，但 JavaScript 會。
因此，若希望子層的 prop 名稱是駝峰式，也就是 `props: ["userName"]`，在父層必須要用 dash (-)隔開，不能直接寫成駝峰式。

O : `<child-component :user-name="name"></<child-component>`
X : `<child-component :userName="name"></<child-component>`
