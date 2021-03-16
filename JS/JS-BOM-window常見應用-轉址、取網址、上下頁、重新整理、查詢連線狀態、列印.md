---
title: '[JS] BOM-window 常見應用-轉址、取網址、上下頁、重新整理、查詢連線狀態、列印'
tags: [JavaScript, BOM]
category: JavaScript
#   - - (所有文章)
#   - - 工程師－攻城路
#     - JavaScript
permalink: posts/2618
date: 2020-12-20 22:48:42
---


BOM （Browser Object Model） - window 常見應用。

<!--more--> 

---

## window 物件

1. `history`
2. `frame`
3. `location`
4. `DOM`
5. `screen`
6. `navigator`

----

## 常見應用：


### history

- 上一頁
    ```javascript
    window.history.back();
    ```

- 下一頁
    ```javascript
    window.history.forward();
    ```

### location

- 轉址
    ```javascript
    window.location.href="http://google.com"
    ```

- 重新整理頁面
    ```javascript
    window.location.reload()
    ```
    ```javascript
    window.location = location.href
    ```

- 取當前網址-例：https://eudora.cc/posts/63534/#more
    ```javascript
    window.location.href     // "https://eudora.cc/posts/63534/#more"
    ```
    ```javascript
    window.location.origin   // "https://eudora.cc"
    ```
    ```javascript
    window.location.protocol // "https:"
    ```
    ```javascript
    window.location.hostname // "eudora.cc"
    ```
    ```javascript
    window.location.pathname // "/posts/63534/"
    ```
    ```javascript
    window.location.hash     // "#more"
    ```

### navigator

- 查詢是否為連線狀態
    ```javascript
    window.navigator.onLine  // true = 連線中、false = 離線狀態
    ```


### 其他

- 列印
    ```javascript
    window.print()
    ```
- 跳轉連結（預設為開啟新視窗，也還有其他參數可控制細節）
    ```javascript
    window.open('http://google.com')
    ```

---

參考資料：
- [JavaScript 入門 - 學徒的試煉 | 六角學院](https://www.hexschool.com/courses/javascript.html)