---
title: '[Vue.js] 實例-ToDoList (基本CRUD.Axios載入預設資料)'
tags: [JavaScript, Vue.js]
category: Vue.js
date: 2020-10-13 11:46:42
permalink: posts/201013

---

示例 用 Vue 實作 ToDoList(CRUD)。

<!--more--> 

> 適用:
> - 略知 Vue.js 結構
> - 知道取 API 資料
  
---

用 Vue.js  實作一個「一眼瞬間」版的 ToDoList。
為什麼叫「一眼瞬間」呢？因為 F5 刷新就沒啦！ 先來做這個最基本連 localStorage 都沒有的 ToDoList，當做 Ｖue.js 應用練習。   
再多加一項初始載入指定的 API（Axios GET)。

---

## [完整栗子 >> Codepen Demo](https://codepen.io/eudora-hsj/pen/WNxQjKp?editors=1111)

<iframe height="450" style="width: 100%;" scrolling="no" title="*Vue.js. - TodoList (+API  Read)" src="https://codepen.io/eudora-hsj/embed/WNxQjKp?height=265&theme-id=dark&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/eudora-hsj/pen/WNxQjKp'>*Vue.js. - TodoList (+API  Read)</a> by Eudora
  (<a href='https://codepen.io/eudora-hsj'>@eudora-hsj</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---

## 練習素材：

- [範例實作前的原始 Template｜六角學院](https://codepen.io/Wcc723/pen/VXRWyg)
- 載入初始資料用的 API： [https://eudora-hsj.github.io/Vue-practice/data/todolist.json](https://eudora-hsj.github.io/Vue-practice/data/todolist.json)
- 記得要引入 Vue.js(v2.x)、Axios

---

## 拆解功能：

1. （data）資料格式定義，每筆待辦項有：'id' / 'title' / 'completed'
    - id 值不可重複
    - completed 為 true / false 
2. 可以讀取（Ｒ）初始資料（API GET）
    
    ![](https://i.imgur.com/HMHerhi.png)

3. 可以新增（Ｃ）待辦項並即時顯示（預設狀態為「未完成」）
    
    ![](https://eudora.cc/img-post/1013-1.gif)

4. 可以編輯（Ｕ）目前的待辦項
    - 更名
    - 點擊時變更完成狀態
    
    ![](https://eudora.cc/img-post/1013-2.gif)

5. 可以刪除（Ｄ）待辦項
    
    ![](https://eudora.cc/img-post/1013-3.gif)

6. 可以一次刪除所有待辦項
    
    ![](https://eudora.cc/img-post/1013-4.gif)

7. 頁籤(Tab)依完成狀態分類清單：全部 / 進行中 / 已完成 
    
    ![](https://i.imgur.com/13RrxoK.png)

8. 計數目前未完成的項，且有變動時即時更新計數

    ![](https://eudora.cc/img-post/1013-5.gif)


--- 

## CODE

(下列 HTML 的部分這邊只截取有應用到 Vue.js 的部分，也就是要觸發事件 / 進行資料綁定的，完整版請看 Codepen)

```html


<div class="container" id="app">
  <input class="form-control" type="text" placeholder="準備要做的任務" 
          v-model="newTodo" @keyup.enter="addTodo"/>
  <div class="input-group-append">
    <button class="btn" type="button" @click="addTodo">新增</button>
    <template v-for="(item, index) in visibilityList">
      <li class="nav-item" :key="index"></li>
      <a class="nav-link" href="#" :class="{ active: visibility == item.value }" 
          @click="(visibility = item.value)">{{ item.name }}
      </a>
    </template>
    <template v-for="(item) in filteredTodos">
      <li class="list-group-item" :key="item.id" @dblclick="editTodo(item)">
        <div v-if="item.id !== cacheTodo.id">
          <input class="form-check-input" :id="item.id" type="checkbox" 
                  @click="changeComplated(item.id)" 
                  v-model="item.completed"/>
          <label class="form-check-label" :class="{ completed: item.completed }"
                  :for="item.id"> {{ item.title }}
          </label>
          <button class="close" type="button" aria-label="Close" 
                  @click="removeTodo(item)">×
          </button>
        </div>
        <input class="form-control" type="text" 
            v-model="cacheTitle" v-if="item.id == cacheTodo.id" 
            @keyup.esc="cancelEdit" @keyup.enter="doneEdit(item)"/>
      </li>
    </template>
  </div>
  <div class="card-footer">
      {{ `還有${activeTodosLength}筆任務未完成` }}
      <a href="#" @click="cleanTodo">清除所有任務</a>
  </div>
</div>
```
     
```javascript
var urlAPI = "https://eudora-hsj.github.io/Vue-practice/data/todolist.json"

var app = new Vue({
    el: "#app",
    data() {
        return {
            newTodo:'',
            todos: [],
            visibilityList: [
                { name: "全部", value: "all" },
                { name: "進行中", value: "active" },
                { name: "已完成", value: "completed" }
            ],
            visibility: 'all',
            cacheTodo: {},
            cacheTitle: '',
        }
    },
    created() {
        this.getList(urlAPI)
    },
    methods: {
        getList(url) {
            axios
                .get(url)
                .then((res) => {
                    this.todos = res.data.data
                })
                .catch((err) => {
                    console.log(err)
                })
        },
        addTodo() {
            let newTodoStr = this.newTodo.trim()
            if (!newTodoStr) {
                return
            }
            this.newTodo = ""
            let submitData = {
                id: Math.floor(Date.now()),
                title: newTodoStr,
                completed: false
            }
            this.todos.push(submitData)
        },
        removeTodo(item) {
            this.todos.splice(this.getIndex(item.id), 1)
        },
        editTodo(item) {
            this.cacheTodo = item
            this.cacheTitle = item.title
        },
        cancelEdit() {
            this.cacheTodo = {}
        },
        doneEdit(item) {
            item.title = this.cacheTitle
            this.cacheTitle = ""
            this.cacheTodo = {}
        },
        cleanTodo() {
            this.todos.splice(0, this.todos.length)
        },

        getIndex(id) {
            return this.todos.findIndex((el) => el.id == id)
        },
        changeComplated(id){
            let index = this.getIndex(id)
            this.todos[index].completed = !this.todos[index].completed
        }
    },
    computed: {
        filteredTodos() {
            let nowTab = this.visibility
            switch (nowTab) {
                case "all":
                    return this.todos.filter((item) => true)
                case "active":
                    return this.todos.filter((item) => !item.completed)
                case "completed":
                    return this.todos.filter((item) => item.completed)
            }
        },
        getNewKey() {
            return Math.max(...this.todos.map((el) => +el.id))
        },
        activeTodosLength() {
            return this.todos.filter((item) => !item.completed).length
        }
    }
})
 ```

---

## 分段說明：

### Vue 基本結構及使用到的屬性：

```javascript
var app = new Vue({
    el: "#app",,
    data(){    // 定義資料 
        
    },
    created(){ // 初始完成 Vue 建立後要執行...
    
    },
    methods:{ // 定義在Vue或頁面中要使用的方法（function）
    
    },
    computed:{ // 進行計算的方法
    
    }
})
```

- 補充資料：[computed vs methods](https://ithelp.ithome.com.tw/articles/10191808)

---

### 定義資料
- 定義初始資料

    ```javascript
    data() {
        return {
            todos: [],
            visibilityList: [  // 3種檢視清單（Tab)
                { name: "全部", value: "all" },
                { name: "進行中", value: "active" },
                { name: "已完成", value: "completed" }
                // name是頁面顯示文字,value是程式中操控的值 
            ],
            visibility: 'all',   // 當前檢視中的清單Tab,預設為全部
            cacheTodo: {},  // 暫存的Todo 
            cacheTitle: '' //暫存的項目名稱
        }
    }
    ```

---
         

### 讀取指定的 API  載入初始資料

- 將 API 網址存成一變數
    ```javascript
    var urlAPI = "https://eudora-hsj.github.io/Vue-practice/data/todolist.json"
    ```
    並且觀察一下 JSON 檔資料結構：  
    ```javascript
    {
        "data":
            [
                {
                    "id": "1",
                    "title": "買牛奶",
                    "completed": false
                },
                {
                    ...
                }
        ]
    }
    ```

- 在 methods 裡定義讀取資料的 function（Axios）    
    ```javascript
    methods:{ 
        getList(url) {
            axios
                .get(url)
                .then((res) => {
                    this.todos = res.data.data
                })
                .catch((err) => {
                    console.log(err)
                })
        },
    }
    ```
- 並且在 Vue 初始建立完成時執行 getList(url)
    ```javascript
    this.getList(urlAPI)
    ```

---

### 可以新增（Ｃ）待辦項

- 在對應的 DOM @dbclick / @keyup.enter 觸發事件
    ```html 
    <button class="btn btn-primary" type="button" @click="addTodo">新增</button>
    ```
    ```html 
    <input class="form-control" type="text" 
           v-model="newTodo" @keyup.enter="addTodo"/>
    ```
- 定義的方法  
    ```javascript
    methods: {
        addTodo() {
            let newTodoStr = this.newTodo.trim()
            if (!newTodoStr) {
                return
            }
            this.newTodo = ""
            let submitData = {
                id: Math.floor(Date.now()),
                title: newTodoStr,
                completed: false
            }
            this.todos.push(submitData)
        }
    }
    ```
---

### 可以編輯（Ｕ）目前的待辦項

- 在對應的 DOM @dbclick 觸發事件
    ```html 
    <li class="list-group-item" :key="item.id" @dblclick="editTodo(item)">
        (略)
    </li>
    ```
- 定義的方法  
    ```javascript
    methods: {
        editTodo(item) {
            this.cacheTodo = item
            this.cacheTitle = item.title
        }
    }
    ```
---
### 可以刪除（Ｄ）待辦項


- 在對應的 DOM @click 觸發事件
    ```html 
    <button class="close" type="button" @click="removeTodo(item)">
    </button>
    ```
- 定義的方法  
    刪除該項，並以 index 與 item 的 id 對應
    ```javascript
    methods: {
        removeTodo(item) {
            this.todos.splice(this.getIndex(item.id), 1)
        }
    }
    ```
---
 
### 可以一次刪除所有待辦項

- 在對應的 DOM @click 觸發事件
    ```html 
    <a href="#" @click="cleanTodo">清除所有任務</a>
    ```
- 定義的方法  
    filter 篩選出 completed 為 false 的資料並回傳筆數
    ```javascript
    methods: {
        cleanTodo() {
            this.todos.splice(0, this.todos.length)
            }
        }
    }
    ```
- 補充資料: [JS-splice() | MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

---

### 頁籤(Tab)依完成狀態分類清單：全部 / 進行中 / 已完成 

- Tab 頁籤內容抓取自 data 裡的 visibilityList  
- @click，visibility　等於該 Tab 的 Value　（all / active / completed　）  
- 並且寫有當前Tab樣式的 active　要維持在 visibility 對應的 Tab
    ```html 
    <template v-for="(item, index) in visibilityList">
        <li class="nav-item" :key="index">
            <a class="nav-link" href="#" 
              :class="{'active' : visibility == item.value }"
              @click="visibility=item.value">
                  {{item.name}}
            </a>
      </li>
    </template>
    ```
- 清單項目抓取自 filteredTodos  的結果（篩選出當前 Tab 的項目）
    ```html
      <template v-for="(item) in filteredTodos">
        <li class="list-group-item">
         （略）
        </li>
      </template>
    ```

- 計算的方法  
    根據當前的 visibility 回傳對應狀態的項目
    ```javascript
    computed: {
        filteredTodos() {
            let nowTab = this.visibility
            switch (nowTab) {
                case "all":
                    return this.todos.filter((item) => true)
                case "active":
                    return this.todos.filter((item) => !item.completed)
                case "completed":
                    return this.todos.filter((item) => item.completed)
            }
        },
    }
    ```
---

### 計數目前未完成的項，且有變動時即時更新計數

- 在對應的 DOM 綁定顯示資料
    ```html 
    <div>{{`還有 ${activeTodosLength} 筆任務未完成`}}</div>
    ```
- 計算的方法  
    filter 篩選出 completed 為 false 的資料並回傳筆數
    ```javascript
    computed: {
        activeTodosLength() {
            return this.todos.filter((item) =>            
                !item.completed).length
            }
        }
    }
    ```
---

### 參考資料：
-  本例子參考自線上課程：[Vue 出一個電商網站｜六角學院](https://www.udemy.com/course/vue-hexschool/)
- [Axios](https://github.com/axios/axios)

---

⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10252979)
