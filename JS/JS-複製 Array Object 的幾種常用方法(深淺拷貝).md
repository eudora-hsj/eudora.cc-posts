---
title: '[JS] 複製 Array / Object 的幾種常用方法（深/淺拷貝）'
tags: [JavaScript, Object, Array]
category: JavaScript
#   - - (所有文章)
#   - - 工程師－攻城路
#     - JavaScript
# permalink: posts/:year:month:day:seconds
permalink: posts/210430
date: 2021-04-30 08:00:42
---

記錄 JavaScript 中，複製 array / object 的常見方法，以及深淺拷貝的差異。

<!--more--> 

---

#### 先備知識：
- **JS 資料型態 ( Data Types )x7**
  1. boolean 布林 （true / false）
  2. null 空
  3. undefined 未定義
  4. number 數值
  5. string 字串
  6. symbol
  7. Object 物件
  - **基本資料型態（Primitive data types）:1 ~ 6**
  - **複合資料型態（Composite data types) :7 - Object**
      - 基本上不屬於基本型態的，都是 Object
      - Array 是 Object 子型別（subtype）：以 `typeof` 查詢會得到 `"object"`


    ---

- **array 與 object**
    ``` js
    // ary
    [1, 2, 3]                  // 一維陣列
    [[1, 1]], [2, 2], [3, 3]]  // 二維陣列
    ```
    ``` js
    // obj
    {   // ---單層物件
        "1": "Amy",
        "2": "Betty",
        "3": "Claire"
    }
    {  // ---多層物件
        "1": {
            "name": "Amy",
            "age": 10
        },
        "2": {
            "name": "Betty",
            "age": 12
        },
        "3": {
            "name": "Claire",
            "age": 8
        }
    }
    ```

---

# "一般狀況下"的賦值動作：

### pass by value  ( 基本型態 )

- 若變數 a、b 為 基本資料型態時 —傳值（pass by value）

    ``` js{1}
    var a = 1
    var b = a
    ```

    a 、 b 記憶體位址獨立， a、b 內容各自修改時並不會互相影響對方的值（b 有開新的記憶體位址並且把 a 的值 copy 過來）。

    ---

### pass by reference  ( 複合型態 )

- 若變數 a、b 為 複合資料型態時（ Object / Array / Function） —傳址（pass by reference）

    ``` js{1}
    var a = { count: 1}
    var b = a
    ```

    a 、 b 記憶體位址共用（ b 沒有建立新的位址，而是引用 a 的記憶體位址） ，此時若賦予 b 新的值 也會影響到 a（循著引用的記憶體位址去改 a ）

    ---

### pass by sharing

在 function 改複合資料型態值的兩種狀況：

``` js{1}
var a = { count: 1}
var b = a
```

- 狀況 1：直接修改屬性值 ＝by reference

    ``` js{2}
    function changValue(val){
        a.count = 2
    }
    changValue(a)

    // b也同時被改為 {count : 2}
    ```

- 狀況 2 : 重新賦值整個 object (object literal) ＝by value

    ``` js{2}
    function changValue(val){
        a = { count: 2}
    }
    changValue(a)

    // b 依然是 {count : 1}
    ```

 

---

## 淺拷貝 ＆ 深拷貝

#### 淺拷貝(Shallow Copy)
  - 複製到同一個參考位址（共用同一個記憶體位址）
#### 深拷貝(Deep Copy)
  - 複製整個值包含至深層，存進獨立的記憶體位置，不影響本來的參考

---

# 對 array  / object 複製“值”的幾種常見方法

## 方法1. `ary.slice(0)`  或`ary.concat()`   (陣列)

- 僅限一維陣列 且 陣列值不含obj

    ``` js{2}
    let ary = [1, 2, 3]
    let newAry = ary.slice(0)         //或let newAry = ary.concat()

    //----
    ary === newAry     // false
    newAry.push(4)     // ary = [1, 2, 3]     newAry = [1, 2, 3, 4]
    ```


    ---

## 方法2. `Array.from(ary)`  (陣列)

- 陣列：pass by value  多維陣列也ＯＫ！

    ``` js{2}
    let ary = [[1,1], [2,2]]
    let newAry = Array.from(ary)

    //----
    newAry.push([3.3])
    newAry[0]=[0,0]       

    // ary = [[1,1], [2,2]]     newAry = [[0,0], [2,2], [3,3]
    ```

    ---


## 方法3. `[...ary] / {...obj}`  ES6展開符  (陣列 / 物件)

- 展開符 `...`  展開陣列再裝進 `[]` 空陣列 （ES6 寫法）

    ``` js{2}
    let ary = [1, 2, 3]
    let newAry = [...ary]

    newAry.push(4)
    // ary = [1, 2, 3]     newAry = [1, 2, 3, 4]
    ```

- 多維陣列也ＯＫ！

    ``` js{2}
    let ary = [[1,1], [2,2]]
    let newAry = [...ary]

    newAry.push([3.3])
    newAry[0]=[0,0]
    // ary    = [[1,1], [2,2]]     
    // newAry = [[0,0], [2,2], [3,3]
    ```

- **`{... obj}` 只能拷貝到物件第一層！**

    ``` js{12}
    let obj = {
    	A: 1,
    	B: {
    		a: '2-1',
    		b: '2-2'
    	},
    	C: {
    		a: '3-1',
    		b: '3-2'
    	}
    }
    let newObj = {...obj}

    //----
    newObj.C.c = "3-3" //參照同個位址,obj也改了 
    newObj.A = 2 //第一層有獨立位址, 不影響 obj
    ```

    <img src="https://i.imgur.com/mGt7jc7.png" style="width: 500px; max-width: 100%;">


    ---

## 方法4. `Object.assign()`  ES6 ( 陣列 / 物件) 

- Array：pass by value  多維陣列也ＯＫ！

    ``` js{2}
    let ary = [[1,1], [2,2]]
    let newAry = Object.assign([],ary)

    //----
    newAry.push([3.3])
    newAry[0]=[0,0]       

    // ary = [[1,1], [2,2]]     newAry = [[0,0], [2,2], [3,3]
    ```

- Object：obj 只有第一層時 - pass by value 

    ``` js{5}
    let obj = {
        a: 1,
        b: 2
    }
    let newObj = Object.assign({},obj)

    //----
    newObj.b = 3
    // obj 維持 = { a: 1,b: 2}
    // newObj   = { a: 1, b: 3 }
    ```
    
    ps. 如果obj 裡面的value 本身已經是被淺拷貝過來的（記錄址而非值），newObj 裡存到的也是址

- Object：第二層開始 pass by reference  （相當於只能拷貝值至 object 第一層）

    ``` js{12}
    let obj = {
        A: 1,
        B: {
            a: '2-1',
            b: '2-2'
        },
        C: {
            a: '3-1',
            b: '3-2'
        }
    }
    let newObj = Object.assign({},obj)
    //----
    newObj.A = 2           //有獨立位址, 不影響 obj
    newObj.C.b = "3-22222" //沒有獨立位址, 影響到 obj
    ```


    <img src="https://i.imgur.com/IxKrlG2.png" style="width: 500px; max-width: 100%;;">

    ---

## 方法5. `JSON.stringify()` / `JSON.parse()` ( 陣列 / 物件) 

- 陣列值/物件值內容不能包含 function 或 RegExp ...等
- `JSON.stringify()` 先轉成字串;再`JSON.parse()` 再轉回原本的 物件/ 陣列
- 陣列與物件都可多維/多層拷貝

    ``` js{2}
    let ary = [[1,1], [2,2]]
    let newAry = JSON.parse(JSON.stringify(ary))

    //----
    newAry.push([3.3])     

    // ary = [[1,1], [2,2]]     newAry = [[1,1], [2,2], [3,3]
    ```

- 不同方法4 ，obj 可拷貝至深層

    ``` js{12}
    let obj = {
        A: 1,
        B: {
            a: '2-1',
            b: '2-2'
        },
        C: {
            a: '3-1',
            b: '3-2'
        }
    }
    let newObj =  JSON.parse(JSON.stringify(obj))
    //----
    newObj.C.b = "3-22222" //有獨立位址, 不影響 obj
    newObj.A = 2           //有獨立位址, 不影響 obj
    ```

    <img src="https://i.imgur.com/dXR91qg.png" style="width: 500px; max-width: 100%;">

    - 不適用於值是 function 的或為 undefined 的（會遺失）。


    ---


## 其他

- 使用  `lodash` 的 `cloneDeep`... 等 library

---

## 結論 - 想拷貝值而非址時

 | Method                                          | Ary<br/>一維  | Ary <br/>含多維 | obj <br/>單層    | obj <br/>含多層 |限制|
 | :------------------------------------------- | :-------------: |:-------------: | :-------------: | :-------------:|  :------------------------------------------- |
 | ` ary.slice(0) ` <br/>` ary.concat()`  |√ | | |  |  限值不含 object ... 等|
 | `Array.from(ary)`                          |√  | √  |  |  |
 | `[...ary]` <br/>` {...obj}`   |√  |√  |√|  |  |
 | `Object.assign([],obj)` <br/>` Object.assign({},obj)`  |√  | √| √|  |  |
 | `JSON.parse(JSON.stringify(ary))` <br/>` JSON.parse(JSON.stringify(obj))` | √| √| √| √   |限值不含 function..等|


---


參考資料：

- [Methods for deep cloning objects in JavaScript - LogRocket Blog](https://blog.logrocket.com/methods-for-deep-cloning-objects-in-javascript/)
- [How to Deep Copy Objects and Arrays in JavaScript](https://javascript.plainenglish.io/how-to-deep-copy-objects-and-arrays-in-javascript-7c911359b089)
- [Object.assign()｜MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
- [重新認識 JavaScript: Day 05 JavaScript 是「傳值」或「傳址」？ - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10191057)
- [[筆記] 談談 JavaScript 中 by reference 和 by value 的重要觀念](https://pjchender.blogspot.com/2016/03/javascriptby-referenceby-value.html)
- [JS 以陣列 Array 的複製談型別（下） - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10221481?sc=rss.iron)
- [Leon的程式心得](https://dotblogs.azurewebsites.net/Leon-Yang/2020/05/27/180435)
- [理解JS的浅拷贝与深拷贝](http://yuanhehe.cn/2016/11/03/%E7%90%86%E8%A7%A3JS%E7%9A%84%E6%B5%85%E6%8B%B7%E8%B4%9D%E4%B8%8E%E6%B7%B1%E6%8B%B7%E8%B4%9D/)
- [JS-淺拷貝(Shallow Copy) VS 深拷貝(Deep Copy)](https://kanboo.github.io/2018/01/27/JS-ShallowCopy-DeepCopy/)
