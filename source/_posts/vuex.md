---
title: vuex
date: 2019-04-14 11:38:39
tags:
  - vuex
  - vue-tutorial
categories:
  - vue
---

## What is Vuex?
`Vue` + flu`x` = `vuex`

特性:

1.  提供**集中狀態管理**，主要核心為 store(倉庫)。當在大型專案中，平行 component 之間通常校頻繁的傳遞 data，若使用 event bus 會需要重複寫很多次，所以需要 vuex。
2.  為**單向資料流**，不可逆。起始點都是 action，所以一切動作都必須在 action 新增方法，才有辦法執行動作。
    <img src="/images/vuex.png" alt="vuex" width="500px">

## 使用步驟

1. 安裝 vuex：`npm install vuex --save`
2. 在 `src` 資料夾新增 `index.js`

```javascript
import Vue from "vue";
import Vuex from "vuex"; // import vuex
Vue.use(Vuex);

const state = {
  counter: 0
};
const mutations = {
  add(state, n) {
    state.counter += n;
  }
};
const getters = {
  count(state) {
    return (state.counter += 100);
  }
};
const actions = {
  addAction(context) {
    context.commit("add", 10); // 執行Vue.Store物件裡的mutations方法，要用commit
  }
};

export default new Vuex.Store({
  state,
  mutations,
  getters,
  actions
});
```

- state: 管理狀態，單一狀態樹 (Single State Tree)
- mutations: 同步改變狀態的方法，**唯一可直接更改 state 的方法**，透過 commit mutation 中的方法來改變 state。Mutation 必須是同步方法，如果需要非同步操作要放在 action 中。和 event 的概念類似，由事件類型 (type) 加上回調函數 (handler，在其中改變 state)組成。 => 有些專案可能會將 mutation.js 分成 type.js(定義 type)及 mutation.js(組合 type 和 handler)
  範例:

```javascript
// type.js
export const APP_INCREASE_LOADING_COUNTER = "APP_INCREASE_LOADING_COUNTER";
export const APP_DECREASE_LOADING_COUNTER = "APP_DECREASE_LOADING_COUNTER";
```

```javascript
// mutations.js
import * as types from "../mutationTypes";

const mutations = {
  [types.APP_INCREASE_LOADING_COUNTER](state) {
    state.loadingCounter += 1;
  },
  [types.APP_DECREASE_LOADING_COUNTER](state) {
    state.loadingCounter -= 1;
  }
};
```

- getters: 處理或計算數據
- actions: 異步改變狀態的方法，通常都是透過 commit mutation 來變更 state。
  其接受的傳入參數：
  - context : 即 Vue.store()本身，具有相同方法及屬性({ dispatch, commit, state})
  - payload : 分發 action 時傳入的任意資料可由此獲得

3. 在 `main.js` 中，要將 store 引入

```javascript
import Vue from "vue";
import App from "./App";
import store from "./store"; // 會自動讀取 /store 下的 index.js

new Vue({
  el: "#app",
  store,
  render: h => h(App)
});
```

4. 取得 vuex 中的 state、mutations、getters、actions

```html
<script>
  import { mapState, mapMutations, mapGetters, mapActions } from 'vuex'
  export default {
      data(){
          return {
              msg:'Hello Vuex',
          }
      },
      computed: {
          ...mapState(['counter']),
          ...mapGetters(['count'])
      },
      methods: {
          ...mapMutations(['add'])
          ...mapActions(['addAction'])
      }
  }
</script>
```

**有些專案會將 state、mutations、getters、actions 個別獨立成檔放在 store 下**

## 注意
**絕對不能在 mutation 之外的地方更動 state**，連 action 也不行。在 strict mode 下，會嚴格執行此規則，任何可能造成在mutation 之外更動 state 的情況，都會報錯（`Error: [vuex] do not mutate vuex store state outside mutation handlers.`)。

且 mutation 必為同步更動，所以也不能在 mutation 中呼叫另一個 mutation，因此當遇到此狀況時，需要用action才可以同時進行兩個 mutation。
