---
title: 當 Vue router 對上 Event Bus 
date: 2019-05-14 20:11:31
tags:
	- vue router
	- Event Bus
	- lifecycle
categories:
	- vue
---

當我們運用 router 將 component 從 A 轉到 B 時，若不使用 router 本身的 params 傳遞 data 給 B，也不使用 vuex 時, 可能會選用 Event Bus。但是!!! 此時 Event Bus 會失效，並無法順利接收到資料，進而呈現在 DOM 上面。

禍源 = > **Lifecycle**

原先一般作法應該會是

> 在 A component

```javascript
 method(){
	this.$bus.emit(....);
 }
```

> 在 B component

```javascript
 created(){
　	this.$bus.on(....);
 }
```

但因為在 A component 通過 $emit 觸發自定義事件時， B component 的 $on 尚未被註冊，所以沒有監聽器接收 A component 的自定義事件。

> A => created() => beforeMount() => mounted() => beforeUpdate()
> => updated() //$emit 觸發自定義事件 
> **A component =======> B component**
> => B--beforeCreate() => created() //$on 註冊
> => beforeMount()
> => **A--beforeDestroy()** => destroyed()
> => **B--mounted()**

**解決辦法:將 `$emit` 放在 A 的 beforeDestroy() 中**
另外!!!要記得將 `$on` 監聽器在 component `destroyed()`時 `$off` 掉，不然重複執行相同的動作時，`$on` 的監聽行為會被重複兩次!!!

參考文章: [Vue 中的 Event bus 跟 Router 撞出新地雷](https://medium.com/@ceall8650/vue%E4%B8%AD%E7%9A%84event-bus%E8%B7%9Frouter%E6%92%9E%E5%87%BA%E6%96%B0%E5%9C%B0%E9%9B%B7-5d3e52545cec)
