---
title: '[JS] 宣告、Function、Hoisting'
tags: [JavaScript, Function, Hoisting]
category: JavaScript
#   - - (所有文章)
#   - - 工程師－攻城路
#     - JavaScript
permalink: posts/26418
date: 2020-09-30 22:48:42
---

關於 JavaScript　中的 function、宣告（var / let / const）、Hoisting 的觀念筆記。

<!--more--> 

---

## Function

一連串的處理、一群指令的集合。

### 定義 function() 起手式

#### 定義有名字的 （一般）function

```javascript
function functionName(參數1, 參數2...) {
    ... 執行內容
　　return 回傳值　（非必要）
}
```
#### 定義沒有名字的 （匿名）function　

```javascript
function(參數1, 參數2...) {
    ... 執行內容
　　return 回傳值　（非必要）
}
```

#### 有名字 V.S 沒名字的 function ?

- 有名字的 function　可更方便的在不同的地方被呼叫。   
- 沒名字的（匿名）function 
    - 可存進變數裡，透過變數被呼叫。  
        ```javascript
        var total = function() {
            ... 
        }
        ```
    - 或透過 IIFE 的方式執行： *（感謝泰安老師補充、Eureka解惑）*
        ```javascript
        (function() {
            ... 
        })()
        ```
- 呼叫時的差異：  
  有名字 function 在其前或後，都可呼叫成功。  
  指給變數的匿名函數，在呼叫時必須在其變數定義行之後才可呼叫。
---

### Function被呼叫時
```javascript
function myFunction(x) {
	return x
}
```
```javascript
console.log(myFunction)
// 印出整個function code
```
```javascript
console.log(myFunction(2)) 
// 印出function回傳值
```

### 基礎寫法
- 定義與呼叫function時一定要加()
- 回傳值要加 return
- return行之後的程式碼都不會執行(return表function結束)

---

### 箭號涵式 Arrow Function
- 函式運算式
    ```javascript
    function show(text){
      console.log(text)
    }
    ```
- 箭號涵式
    - 寫法1 : (參數)=>(回傳值)
        > 宣告 函數名稱 (參數1,參數2) => ( 回傳值 )
        - 回傳值可以省略return
        參數只有一個的時候可以省略括號
        > 宣告 函數名稱 參數1 => ( 回傳值 )
        - 參數只有1個的時候可以省略()
        > 宣告 函數名稱 () => ( 回傳值 )
        - 沒有參數的時候不能省略括號
    - 寫法2 : (參數)=>{涵式內容}
        > 宣告 函數名稱 (參數1,參數2) => {  
        >   涵式內容
        >   ...
        >
        > }

    - 例1:
        ```javascript
        var show = (text) =>{
          console.log(text)
        }
        ```
    - 例2 (內裡匿名涵式):
        ```javascript
        setTimeout(()=> { 
            console.log('text')
        }),1000);
        ```
    

---

## Hoisting 提升

- 先呼叫 function 才定義 function，也能順利執行
    ```javascript
    var fun = (name) =>{
      console.log(name)
    }

    fun("Amy");  /*Amy"*/
    ```
- 先使用變數才宣告 var 時，不會噴錯、能順利執行 = undefined  
    - 因為只有提升宣告、沒有提升定義值
        ```javascript
            console.log(num)
            var num=1   // 是"undefined"、不是"Error"也不是1
        ```
        ![](https://i.imgur.com/ExOZclu.png)

- 其他示例
    ```javascript
    // 先使用變數再let宣告與賦值
    console.log(num1)
    let num1=1 
    // Uncaught ReferenceError: Cannot access 'num1' before initialization  
    ```
    ```javascript
    // 先使用變數再var宣告與賦值
    console.log(num2)
    var num2=1   
    // undefined
    ```
    ```javascript
    // 先使用變數才賦值但無宣告
    console.log(num3)
    num3=2
    // Uncaught ReferenceError: num3 is not defined 
    ```
    ```javascript
    // 先使用變數才var宣告但無賦值
    console.log(num4)
    var num4   
    // undefined
    ```
    ```javascript
    // 先使用變數才let宣告但無賦值
    console.log(num5)
    let num5   
    // Uncaught ReferenceError: Cannot access 'num5' before initialization 
    ```

---
## Scope 作用域

- global scope － 包含function外（全域）
- function scope - function內
- block scope  - block 內

---

## 宣告變數＆常數－var / let / const

|               | var                     | let       | const              |
|:------------- |:----------------------- | --------- |:------------------ |
| 意義          | 宣告變數                | 宣告變數  | 宣告常數           |
| 宣告時        | 可以先不指定值          | ← (同var) | 必須指定值         |
| 宣告後        | 可再次指定值            | ← (同var) | 不可改變值         |
| 宣告後        | 可再次宣告            | 不可再次宣告 | 不可再次宣告         |
| 範例          | `var x`<br/>`var x = 2` | ← (同var) | `const PI=3.14159` |
| Scope<br/>作用域 | 該**涵式區塊**                    | 該**程式區塊**{大括號內}<br/>*包含迴圈/判斷*      |  ← (同let)               |

- 變數宣告不用指定類型  
  可以隨時改變變數值的類型(儘量避免)  
  型別資訊只存在在值或物件本身，變數本身沒有型別
- 早期只能用var宣告變數，ES6增加 let、const
- 如果沒有宣告而直接賦值(num=2)也會成功  
  因為 JS 自動視為全域變數宣告（但最好不要這樣）

```javascript
print=(content)=>{
  console.log(content)
}
```
- Var
    1. var 沒有 function 時，scope 為整塊
        ```javascript
        for(var i=0 ; i<5 ; i++){
          print(i)  //成功取得 i (=1、2、3、4)
        }
        print(i)    //成功取得 i (=5)
        ```
    2. var 在 function 內時，scope = function 內  
        function 外讀不到
        ```javascript
        function test(){
          for(var i=0 ; i<5 ; i++){
            print(i)  //成功取得 i (=1、2、3、4)
          }
        }
        print(i)    //無法取得 i
        ```
- Let
    -  let scope 只在{  }內  
        {  } 外就讀不到了
        ```javascript
        for(let i=0 ; i<5 ; i++){
          print(i)  //成功取得 i (=1、2、3、4)
        }
        print(i)    //無法取得 i
        ```
---


參考資料：
- [arrow function|MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [Hoisting|MDN](https://developer.mozilla.org/zh-TW/docs/Glossary/Hoisting)
- [IIFE|MDN](https://developer.mozilla.org/zh-TW/docs/Glossary/IIFE)
- [ASTRO X 五倍紅寶石 全端工程師實戰訓練營 | 蘇泰安](https://taian.su/)
---
