---
title: Use LocalStorage with Vuex
date: 2019-08-02 15:50:51
tags:
  - localStorage
  - vuex
catogories:
  - vue 
---
## What is localStorage and Vuex?
相關文章可參考我之前寫的 {%post_link web-storage%}、{%post_link local-Storage%}、{%post_link vuex%}


## Use LocalStorage with Vuex
目標：希望在一進入 app 或網頁時，就可以抓取 localStorage 所存的資料，並統一由 Vuex 進行集中的狀態管理

#### 設定 Vuex Store，建立 mutation 來改變 state
``` javascript
// store.js
const store = new Vuex.Store({
  state: {
    user: {
      name: '',
      favorite: ''
    }
  },
  mutations: {
    setUserData(state, { userData }) {
      state.user.name = userData.name;
      state.user.favorite = userData.favorite;
    }
  }
});
```

#### 在取得資訊要存進 localStorage 的頁面，使用 mutation
``` html
<!-- page -->
<html>
...
</html>
<script>
export default {
  data () {
    return {
      userData: {
        name: '',
        favorite: ''
      }
    }
  },
  created () {
    // 取得 userData
    this.userData = this.$store.state.userData
  },
  methods: {
    // 首次編輯使用者資訊或更新使用者資訊會呼叫此 method
    saveUserData () {
      this.$store.commit({
        type: 'setUserData',
        userData: this.userData,
      });
    }
  }
}
</script>
```
#### 使用 Subscribe 偵測此 mutation，一旦此 mutation 被呼叫就重新存 localStorage
**使用 plugin 在 store 中註冊 Subscribe，只要 store 一被初始化，此 plugin 就會被呼叫，並開始監聽 mutation**
[Plugins官方文件](https://vuex.vuejs.org/guide/plugins.html)

``` javascript
// store.js
const localStoragePlugin = store => {
  // called when the store is initialized
  store.subscribe((mutation, state) => {
    window.localStorage.setItem('userData', JSON.stringify(state.userData))
  })
}
const store = new Vuex.Store({
  // ...

  //將 localStoragePlugin 引用進來
  plugins: [localStoragePlugin]
});

```

**Subscribe**
官方文件：[Subscribe](https://vuex.vuejs.org/api/#subscribe)
Vuex.Store 的 Instance method，負責監聽他所訂閱的 mutation，若該 mutation 有更動會馬上被呼叫

``` javascript
store.subscribe((mutation, state) => {
  console.log(mutation.type) // 要監控的 mutation
})
```
#### 最後新增 initLocalStorage mutation，在剛進入 app 或網頁時，看 localStorage 有沒有存資料，如果有就存進 state 中，沒有就用 api 抓

``` javascript
// store.js
const localStoragePlugin = store => {
  ...
}
const store = new Vuex.Store({
  // ...

  mutations: {
    ...,
    initLocalStorage (state){
      if (window.localStorage.getItem('userData')) {
        state.userData = JSON.parse(window.localStorage.getItem('userData'))
      }
    }
  }
  
});

```

``` html
<!-- app.vue -->
<html>
...
</html>
<script>
export default {
  data () {
    return {
    }
  },
  created () {
    this.initLocal()
    // 接著就判斷 this.$store.state.userData有沒有資料，沒有就用api抓，再存進 store
  },
  methods: {
    initLocal () {
      this.$store.commit({
        type: 'initLocalStorage',
      });
    }
  }
}
```