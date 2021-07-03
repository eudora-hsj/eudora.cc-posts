---
title: '[JS] 處理字串與數值的相關方法'
tags: [JavaScript]
category: JavaScript
#   - - (所有文章)
#   - - 工程師－攻城路
#     - JavaScript
permalink: posts/210120
date: 2021-01-20 22:48:42
---

關於 JavaScript　中的處理字串與數值的常見方法，如 `slice` 、`split`、`concat`...等。

<!--more--> 

---

## 字串擷取/取代

| Method | Do | Remark |
| -------- | -------- | -------- |
| `slice(2,3)`  |擷取字串（起,終）|擷取字串第2~3個|
| `substring(3,5)`  |擷取字串（起,終） |同slice但參數不可寫負|
| `substr(1,3)`  |擷取字串（起,長度） |從第1個開始擷取3個（長度不得為負）|
| `replace("abc","def")`  |字串內的abc改為def |大小寫有別<br/>是返回新字串|
| `charAt(n)`   |取字串內第Ｎ個字 ||
| `charCodeAt()`   |取字串內第Ｎ個字的unicode ||

 1. slice / substr 參數設負代表倒數第Ｎ個（IE8不支援）  
 2. slice / substr / substring 若沒寫第2個參數＝擷取到底
 3. replace（/abc/i,"def"）第一個參數去引號並加入正規表達式/i則可通用大小寫


## 字串拆開/組合/清除空白

| Method | Do | Remark |
| -------- | -------- | -------- |
| `split("_")`   |依特定_字拆解成一個陣列 |`split("")`參數空時<br/>相當於直接把所有字拆開|
| `concat()`   |連接字串 | `"Hello".concat.(" ","World" )`|
| `trim()`   |刪除字串內的左右兩邊空白符 ||

## 字串大小寫轉換

| Method | Do | Remark |
| -------- | -------- | -------- |
| `toUpperCase()`  |字串轉大寫||
| `toLowerCase()`  |字串轉小寫||

## 數值轉進位制

| Method | Do | Remark |
| -------- | -------- | -------- |
| `toString(16)`   |數值轉Ｎ進制 |128.toString(16) = 80 (128轉16進制）|


## 數值處理

| Method | Do | Remark |
| -------- | -------- | -------- |
| `Number(x)`    | 回傳數字     | 變數轉為數值,無法轉為數字時回傳NaN     |
| `parseFloat(x)`    | 回傳數值含浮點數     | -     |
| `parseInt(x)`    | 回傳整數值     | -     |

---

參考資料：
- [Useful string methods|MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Useful_string_methods)

---
