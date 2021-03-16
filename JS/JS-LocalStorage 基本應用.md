---
title: '[JS] LocalStorage 基本應用'
tags: [JavaScript, LocalStorage]
category: JavaScript
#   - - (所有文章)
#   - - 工程師－攻城路
#     - JavaScript
permalink: posts/26218
date: 2021-01-12 22:48:42
---

簡介 JavaScript 中的 LocalStorage 基本操作。

<!--more--> 

## LocalStorage

儲存在瀏覽器內對於特定網頁的Local資料庫，關閉網頁、再次開啟網頁時仍可存取。
使用ＪＳ清除或者使用者於瀏覽器進行清除資料才會不見。

![Image](https://i.imgur.com/nv6iYeC.png)

---

## 基本語法: `setItem()` / `getItem()` / `removeItem()` / `clear()`


- 儲存特定資料

    ```javascript
    localStorage.setItem('key', value)
    ```

- 取出特定資料

    ```javascript
    localStorage.getItem('key')
    ```

- 刪除特定資料

    ```javascript
    localStorage.removeItem('key')
    ```

- 清除所有資料

    ```javascript
    localStorage.clear()
    ```

---

## 資料型態為字串

- 儲存於 LocalStorage 的資料只能是字串，故：
    - 想存 Array 或 Object 時，必須先轉型為 String
    - 自 LocalStorage 取出的資料都是字串，必須轉型回來，才能對其操作 Array / Obj 方法


- 轉字串
    ```javascript
    JSON.stringify(el)
    ```


- 字串轉回 Array / Obj
    ```javascript
    JSON.parse(el)
    ```

- 查詢資料格式
    ```javascript
    typeof(el)
    ```

--- 

## [例1] 輸入名字儲存至 LocalStorage，並自 LocalStorage 內取值顯示於頁面

<iframe height="200" style="width: 100%;" scrolling="no" title="*[JS] Local Storage" src="https://codepen.io/eudora-hsj/embed/yLaROgK?height=265&theme-id=light&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/eudora-hsj/pen/yLaROgK'>*[JS] Local Storage</a> by Eudora
  (<a href='https://codepen.io/eudora-hsj'>@eudora-hsj</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### HTML
```HTML
<p>Hi!<span class="showName"></span></p>
<label>Name</label>
<input class="name" type="text"/>
<button id="submit">Submit</button>
```
### JavaScript
```javascript
function saveName(){
    let dataName = document.querySelector('.name').value
    localStorage.setItem('userName', dataName)
}
```
- 取 input 內容存到 localStorage
- `localStorage.setItem('key', value)`


<br>

```javascript
function showName(){
    let nameDom = document.querySelector('.showName')
    nameDom.innerHTML = localStorage.getItem('userName')
}
```

- 從 LocalStorage 裡取值並顯示在指定的 DOM
- ` localStorage.getItem('userName')`


<br>

```javascript
showName();
```
- 一開始就先執行showName（輸入過一次，下次再瀏覽此網頁時也顯示名字）

<br>

```javascript
let btnSubmit = document.querySelector('#submit')
btnSubmit.addEventListener('click', function(){
    saveName();
    showName();
})
```
- 定義按鈕觸發事件：儲存輸入的名字、更新名字
  
<br>

---


## [例2] 非字串資料存進與讀取

```javascript
var classmate = [
    {
        01: 'Eudora',
        02: 'Amy',
        03: 'Betty'
    }
]
```

1. 直接存進 LocalStorage 會變字串 [object object]
    ```javascript
    localStorage.setItem('classmate': classmate)
    ```
    ![Image](https://i.imgur.com/BnWrYPV.png)

<br>

2. `JSON.stringify`轉為字串後再存才能正確存進資料
    ```javascript
    localStorage.setItem('classmate', JSON.stringify(classmate))
    ```
    ![Image](https://i.imgur.com/XqpBMas.png)

<br>

3. 直接取出時，資料是字串，需透過`JSON.parse`轉型回來，：
    ```javascript
    typeof(localStorage.getItem('classmate'))              // > string
    typeof(JSON.parse(localStorage.getItem('classmate')))  // > object
    ```
--- 


參考資料：
- [JavaScript 入門 - 學徒的試煉 | 六角學院](https://www.hexschool.com/courses/javascript.html)

- [LocalStorage｜MDN](https://developer.mozilla.org/en-US/docs/Web/API/Storage)
- [JSON.stringify()｜MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
- [JSON.parse()｜MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)

--- 
