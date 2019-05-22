---
title: DOM 沒有在 Array Update 後更新
date: 2019-05-22 15:36:42
tags:
  - reactivity
categories:
  - vue
---

### Why DOM 沒有在 Array Update 後更新??

類似問題: [https://stackoverflow.com/questions/39794632/vue-js-is-not-updating-the-dom-after-updating-the-array](https://stackoverflow.com/questions/39794632/vue-js-is-not-updating-the-dom-after-updating-the-array)

範例情境:

```html
<div v-for="(p, i) in phoneData" :key="i">
  {{ p.name }} {{ p.number }} {{ p.battery }}
</div>
```

```javascript
  export default {
    data() {
      return {
        phoneData: [{ id: 1, name: "001" }, { id: 2, name: "002" }]
      };
    },
    mounted() {
      self = this;
      self.getPhone();
    },
    method:{
      getPhone(){
        // 透過 API 取得所有 Phone 的 data
        Axios.get.phones().then(function(res) {
          if (res.data.data.length > 0) {
            self.phoneData = res.data.data;
            // phoneData: [{ id: 1, name: "001",number: "99298384" }, { id: 2, name: "002",number: "992939475" }]

            // 因為需要更詳細的資訊(e.g. battery, SIM ...)，而這些資訊需透過另一支 API 獲得，所以要再 API request 一次
            //且這支 API 需用個別 id 抓，一次只能抓到一個 phone 的詳細資訊
            self.phoneData.foreach((p)=>{
              self.getPhoneDetail(p)
            })
        })
        .catch(function(error) {
          console.log(error);
        });
      },
      getPhoneDetail(p){
        Axios.get.phoneDetail(p.id).then(function(res) {
          if (res.data.data.length > 0) {
            p.battery = res.data.data.battery;
            p.SIM = res.data.data.SIM;

        })
        .catch(function(error) {
          console.log(error);
        });
      }
    }
  };

```

在最後 API response 都完成後，下 `console` 取得的 `phoneData` 資料都有抓到，`phoneData: [{ id: 1, name: "001",number: "99298384",battery:"90%", SIM: "dual" }, { id: 2, name: "002",number: "992939475",battery:"80%", SIM: "dual"}`，但在 DOM 上卻只顯示 `name`和 `number`的值，`battery`並沒有值!!!

原因=> **Vue 的 Reactivity( 響應式原理 )**
詳細內容: [為什麼畫面沒有隨資料更新 - Vue 響應式原理（Reactivity）](https://pjchender.blogspot.com/2017/05/vue-vue-reactivity.html)
在 `data(){}`中沒有被註冊到的物件，就不會有 reactive。雖然一開始有註冊 `phoneData`，但只有註冊他其中的兩個 property(id 和 name)，後來加上去的其他屬性都沒有被註冊，所以沒有不會響應式更新，所以 vue 監聽不到他的值已被 update。
而 `number`的值為何會有呢? 因為 `number`是在 DOM render 前就取得，所以會被渲染出來。

解決方式 =>

1. 在 `data(){}` 中，把要 reactive 的所有 property 都註冊
2. 動態添加新的響應式屬性 `Vue.set(Object,key,value)`

```javascript
      getPhone(){
        // 透過 API 取得所有 Phone 的 data
        Axios.get.phones().then(function(res) {
          if (res.data.data.length > 0) {
            self.phoneData = res.data.data;

            self.phoneData.foreach((p,i)=>{
              self.getPhoneDetail(p,i)
            })
        })
        .catch(function(error) {
          console.log(error);
        });
      },
      getPhoneDetail(p,i){
        Axios.get.phoneDetail(p.id).then(function(res) {
          if (res.data.data.length > 0) {
            self.$set(self.phoneData[i],"battery",res.data.data.battery);
            self.$set(self.phoneData[i],"SIM",res.data.data.SIM);
        })
        .catch(function(error) {
          console.log(error);
        });
      }
```
