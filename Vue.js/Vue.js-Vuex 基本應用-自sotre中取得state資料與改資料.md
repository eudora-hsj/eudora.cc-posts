---
title: '[Vue.js] Vuex-新手上路-自 store 中取得與修改資料 (state)'
tags: [JavaScript, Vue.js, Vuex]
category: Vue.js
date: 2021-04-27 23:06:42
permalink: posts/210427

---

示例 透過 Vuex 讀取與修改 store 內的 state。

<!--more--> 

> 適用:  
> - 會基本的 Vue 應用（使用 data / computed / method / 插值... 等） 
  
---


## 無 Vuex 時資料傳遞的作法

上傳下：props in  
下傳上：emit out  
同層級：event bus （簡單情境, 資料量不大時）  
或是透過全域變數，但是全域變數無法雙向綁定  
( 可參考 [無 Vuex 的 Components 間的各種資料傳遞](/posts/210303/) )

---

## Vuex 的運作原理與流程

![Image](https://i.imgur.com/OVrE7Xn.png)

1. 在 `component` 中以 `dispatch` 方法去觸發 `action` 事件  
2. `action` 裡處理同步/異步（如 ajax / setTimeout..等）事件操作  
（ 需要打 API 來取得資料的話，也在此處理）  
並將資料 `commit` 至 `mutation`  
3. 讓 `mutation` 去改變 `State` (資料)  
4. `state` 再回應到 `component` 裡進行 `Render`  

---

## Vuex 的組成

### 核心 - store 倉庫

- component 從 store 中讀取資料狀態 (state)

### 1. state（data）

- 響應式的資料狀態儲存, 資料狀態變化時，有用到的 component 都會即時更新

### 2. action（methods）

- 操作同步或異步事件的處理但不直接修改資料（state）
- 是透過`commit`  → 呼叫 `mutation` 改變 state

### 3. getter（computed）

- 加工資料呈現
- 同 computed 一樣會被緩存、依賴值變更了才會重新計算

### 4. mutation

- 改變`state` 
- 只處理同步函數：不要在這進行非同步的動作（例如 setTimeout / 打 API 取遠端資料...等）

---


> 以下以 CLI 環境為例
## 4-1.安裝

#### 安裝

1. 安裝 Vuex : `npm install vuex --save`  / `yarn add vuex`

    <!-- - 或插入 ＪＳ：
    ```js
    <script src='https://cdnjs.cloudflare.com/ajax/libs/vuex/4.0.0/vuex.cjs.js'></script>
    ``` -->

2. 引入至專案 `src/main.js`

    ```js{2,4}
    ...
    import Vuex from 'vuex'

    Vue.use(Vuex)
    ```

<!-- Ps. Vuex requires Promise , 如果想要相容的瀏覽器沒有 promise (例如 IE)，要另外再擴充 promise 套件（[es6-promise](https://vuex.vuejs.org/zh/installation.html#promise)） -->


---

## 4-2.應用-從 store 中取 state 資料

#### Step1. `src`下 新增檔案 `store/index.js`

- src/ store / index.js

    ```js
    import Vue from 'vue'
    import Vuex from 'vuex'

    Vue.use(Vuex)

    export default new Vuex.Store({
      state: {
        test: 'test data'
      }
    })
    ```

- 修改 `src/main.js`

    ```js{1,6}
    import store from './store'
    ...
    ...
    new Vue({
      el: '#app',
      store,                // -> store: 'store'
    	...
    })
    ...
    ```
    
    <!-- ![Image](https://i.imgur.com/neLeeCl.png) -->


#### Step2. `computed` 內增加取得資料的方法

- component - script 內以 `this.$store.state.＿＿` 取得 store 內的資料

    ```js{4}
    ...
    computed: {
    	test () {
            return this.$store.state.test
        }
    }
    ...
    ```

    <!-- - 可以取與 sotre 內的 state 資料名一致 -->
- component - template 引入

    ```js
    {{test}}
    ```

---

## 4-3.應用-修改 store 中的 state 資料

### 方法1. 在 componet  中直接修改（最好不要這這麼做）

- 例： `<button @click = "___">Change</button>`

    ```js{1,4}
    <...@click="changeHandler()'">
    ...
    changeHandler() {
    	this.$store.state.test = 'balabala'
    }
    ```

    或

    ```js
    < ...@click="$store.dispatch('updateTest','balabala')">
    ```

### 方法2. Vuex: dispatch -> [action] -> commit -> [mutation]

- **Step1. stroe/index.js 增加 `actions` 與 `mutations`  物件**

    ```js{3,6,9}
    ...
    export default new Vuex.Store({
        state: {
            ...
        },
        actions: {
        
        },
        mutations: {
        
        },
    })
    ```

- **Step2.  定義 `actions` 與 `mutation`**
    - action 裡將接收到的資料 commit 至 mutation
    - mutation 內將 action commit 進來的資料傳給 state （修改 state）

    ```js{3-5,8-10}
    ...
    	actions: {
    		updateTest(context, status) {
    			context.commit('TEST', status)     // mutation 中定義方法
    		}
    	},
    	mutations: {
    		TEST(state, status) {      //status -> payload （載荷）
    			state.test = status;
    		}
    	},
    ...
    ```

    - 關於 [Action](https://vuex.vuejs.org/zh/guide/actions.html)  ｜ 關於 [Mutation](https://vuex.vuejs.org/zh/guide/mutations.html)


- **Step3.  component 中修改資料的方式改寫用`dispatch`**

    dispatch 觸發 action 事件, 並傳遞內容

    ```js{4}
    <...@click="changeHandler()'">
    ...
    changeHandler() {
    	this.$store.dispatch('updateTest','balabala')
    }
    ```

    ```js
    < ...@click="$store.dispatch('updateTest','balabala')">
    ```


### 差異

- 應避免使用方法1, （從 DevTool Vue 工具裡的 Vuex 裡觀察，方法 1 並沒有修改到 store state）
<!-- - DevTool Vuex 中 mutation 區，以方法1 沒辦法操作到 -->


## 4-4.應用-getters :資料加工

- Step1. getters 中新增一個方法與回傳值（同 computed 用法）

    ```js{13,14,15}
    ...
    export default new Vuex.Store({
      state: {
        text: '...'
      },
    	actions: {
    		...
    	},
    	mutations: {
    		....
    	},
    	getters: {
            textLength: state => {
                return state.test.length
            }
      }
    })

    ```

- **Step2.component中** `$store.getters.___` **可直接取得資料**

    ```js
    {{$store.getters.textLength}}
    ```

---

## 練習簡單的例子：
> 1. 先載入預設的名字
> 2. 計數名字字數
> 3. 使用者輸入新名字按下 Enter 後修改名字。
> 4. 計數名字字數也應及時更新

### Demo
[> CodeSandbox]([https://codesandbox.io/s/vuex-jichuyingyong-zistorezhongqudestate-getter-ziliao-touguo-action-mustation-xiugai-state-n99w0?file=/src/store/index.js])

<iframe src="https://codesandbox.io/embed/vuex-jichuyingyong-zistorezhongqudestate-getter-ziliao-touguo-action-mustation-xiugai-state-n99w0?fontsize=14&hidenavigation=1&module=%2Fsrc%2Fstore%2Findex.js&theme=dark&view=preview"
     style="width:100%; height:280px; border:0; border-radius: 4px; overflow:hidden;"
     title="Vuex-基礎應用-自store中取得state / getter 資料 &amp; 透過 action mustation 修改 state"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>

<iframe src="https://codesandbox.io/embed/vuex-jichuyingyong-zistorezhongqudestate-getter-ziliao-touguo-action-mustation-xiugai-state-n99w0?fontsize=14&hidenavigation=1&module=%2Fsrc%2Fstore%2Findex.js&theme=dark&view=editor"
     style="width:100%; height:600px; border:0; border-radius: 4px; overflow:hidden;"
     title="Vuex-基礎應用-自store中取得state / getter 資料 &amp; 透過 action mustation 修改 state"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

> (點左上角選單按鈕可以展開目錄欄，瀏覽檔案)

---

## DevTool-Vue 中的 Vuex 面板

![Image](https://i.imgur.com/tMO4XOS.png)

有透過 action 跟 mutation 操作，會多了 mutation 欄位, 且 也能紀錄變化歷程


![Image](https://i.imgur.com/buXwk6S.png)

---

## 開啟 Vuex 嚴謹模式

- stroe/index.js
    開啟嚴謹模式：`strict: true`
    ```js{2}
    export default new Vuex.Store({
        strict: true,
        state: {
            ...
        },
        ...
    })
    ```

    嚴謹模式下，若你在 mutation 之外的地方直接改變 state 內容，會出現 error  
    *（在 component 內或 action內 寫都不行！）*


---

## (參考資料)

-  [Vuex 是什么？ | Vuex](https://vuex.vuejs.org/zh/)  
- [Vue 出一個電商網站 - 第 13 節 Vuex](https://www.udemy.com/course/vue-hexschool/learn/lecture/11240744#overview)