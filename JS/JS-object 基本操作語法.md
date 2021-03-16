---
title: '[JS] Object 物件基本操作'
tags: [JavaScript, Object]
category: JavaScript
#   - - (所有文章)
#   - - 工程師－攻城路
#     - JavaScript
# permalink: posts/:year:month:day:seconds
permalink: posts/26138
date: 2021-01-14 08:00:42
---

記錄 JavaScript 中自定義物件(object)常用基本操作。

<!--more--> 

## 關於 Object {} 物件

- 物件.屬性=屬性值  
    ```javascript
    object.type = value
    ```
  物件.方法(參數)
    ```javascript
    object.method()
    ```

    - 相同物件都有相同的屬性、不同的屬性值
    - 相同物件都有相同的方法可以用


- name(key) & Value 成對 
    ```javascript
    object = {name1: value1, name2: value2, ...}
    ```

- value 可以裝什麼？  
（屬性）1. 原生的值  （boolean / number / string ... 等）   
（屬性）2. 物件 object  
（方法）3. 函式 function  


- 例：

    ```javascript
    var member = {
        firstName: "Eudora",
        lastName: "Huang",
        fullName: function(){
             return this.firstName + " " + this.lastName
        }
    }
    console.log(member.fullName())
    //結果 :  "Eudora Huang"
    ```
    - 注意：用箭頭函示寫 value 裡的 function 時，this 會是 undefind(this的初始值) 而非該函數擁有者(此例為 member)
    - 取值時若為 function 必須要加 `( )`，不然會輸出整段 fucntion code（參行８取fullName時後面加括弧）

<br>

---

## 基本操作語法


### `new Object()` 建立 object

- 建立一個空物件
    ```javascript
    let obj = {}
    ```
- 建立一個物件並定義key & value 
    ```javascript
    let obj = new Object();
        obj.key1 = 'value1';  //或 obj["key1"] = 'value1';
        obj.key2 = 2;         //   obj["key2"] = 2;
        obj.key3 = 'value3';  //   obj["key3"] = 'value3';
    ```
    或
    ```javascript
    let obj = {
        key1: 'value1',
        key2: 2,
        key3: 'value3',
    }
    ```
- object      
    ```javascript
    obj
    // { key1: 'value1', key2: 2, key3: 'value3' } 
    ```

<br>

### `Object.values()` 取 object 值

- 取所有的value
    ```javascript
    Object.values(obj)
    // ['value1', 2, 'value3']
    ```
- 取特定的value
    ```javascript
    obj.key1     
    // 'value1'
    ```
    - 用` . `的方式只能以 key 取
    ```javascript
    obj['key1']    
    // 'value1'
    ```
    - 用`[ ]`的方式，`[ ]`裡面可以放變數或判斷式
    - 如果單純只放key，要加引號 `' '`


<br>

### `Object.keys()` 取 object 屬性（key）

- 取所有的key
    ```javascript
    Object.keys(obj)   
    //['key1', 'key2', 'key3']
    ```
- 取第Ｎ個的key (從0開始)
    ```javascript
    Object.keys(obj)[0]   
    //'key1'
    ```

<br>

### `delete` 刪除 object 屬性（key）

- delete刪除特定的key
    ```javascript
    delete obj.key1
    ```

<br>

### `Object.entries(obj)`、`Object.fromEntries()`  轉型應用

- object 轉成 array of array           
    ```javascript
    Object.entries(obj)
    //  [ [ 'key1', 'value1' ], [ 'key2', 2 ], [ 'key3', 'value3' ] ] 
    ```
- array of array 轉回 Object
    ```javascript
    Object.fromEntries(Object.entries(obj))
    // { key1: 'value1', key2: 2, key3: 'value3' } 
    ```


---

參考資料：
- [JS-Object｜w3school](https://www.w3schools.com/js/js_objects.asp)
- [[筆記] 物件是什麼？method 是什麼？談談 JavaScript 中的物件建立(Object) - Part 1｜PJCHENder](https://pjchender.blogspot.com/2016/01/javascriptobject.html)
- [[筆記] 物件是什麼？method 是什麼？談談 JavaScript 中的物件建立(Object) - Part 2｜PJCHENder](https://pjchender.blogspot.com/2016/01/javascriptobject-part-2.html)