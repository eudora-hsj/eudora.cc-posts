---
title: '[Ajax] 以 GET 方法讀取 JSON 文件'
tags: [JavaScript, Ajax, XMLHttpRequest, Axios, API, jQuery]
category: JavaScript
#   - - (所有文章)
#   - - 工程師－攻城路
#     - JavaScript
#   - - 工程師－攻城路
#     - Ajax
# banner_mask_alpha: 0.5
# comments: true
# banner_img: https://i.imgur.com/VBg9vAF.png
# index_img: https://i.imgur.com/VBg9vAF.png
permalink: posts/26119
date: 2020-07-22 15:44:36
---
<div class="fs-s mb-4r">    

本篇以 
- GET 方法串接 JSON 文件內容示例。
- 原生JavaScript、jQuery、Axios 三種寫法供參考。
<!--more--> 
適用於
- 有基本的 JavaScript 應用能力。
- 知道什麼是 Ajax 。
- 知道透過 API 串接文件的用途。

</div>

<!-- # Ajax應用 (1)- 以 GET 方法讀取 JSON 文件 -->

- 可至[政府資料開放平台](https://data.gov.tw/)取得 JSON 格式的 API  
- 下列範例印在console裡確認是否串接成功

    ![](https://i.imgur.com/VBg9vAF.png)

## 1. XMLHttpRequest

### 示例
```javascript
var dataUrl= "https://cloud.culture.tw/frontsite/trans/SearchShowAction.do?method=doFindTypeJ&category=6"
var xhr = new XMLHttpRequest()
xhr.open('GET',dataUrl, true)
xhr.send()
xhr.onload = function(){
    var data = JSON.parse(this.responseText);
    console.log(data);
}
```
```javascript
//↑行5可以改成
xhr.onreadystatechange = function(){
    if(this.readyState === 4 && this.status === 200){
        var data = JSON.parse(this.responseText);
            console.log(data);
    }
}
```

### 分段說明:
```javascript
// 1.設一個變數把API的URL存起來
var dataUrl= "API的URL"

```
```javascript
// 2.new一個XMLHttpRequest物件(以此物件的方法進行資料請求) 
var xhr = new XMLHttpRequest()
```
```javascript
// 3.以GET方法開啟一個請求
//open('Method',API的URL,預設值為true非同步進行)
xhr.open('GET',dataUrl, true)
```
```javascript
// 4.送出請求(若為GET參數不填或填null)
xhr.send() 
```
```javascript
// 5-1 或直接用 onload => 資料接收/送出成功後執行的function
xhr.onload = function () {
    var data = JSON.parse(this.responseText);
    console.log(data);
}
```
```javascript
// 5-2.寫一個function處理狀態改變時(onReadyStateChange)
//   0=執行前    1=讀取中   2=已讀取  3=資訊交換中  4=完成
//   status(HTTP狀態碼):200 正常完成
xhr.onreadystatechange = function(){

    // 如果完成(readyState=4 , 且HTTP狀態正常 status=200)
    if(this.readyState === 4 && this.status === 200){
    
        // 將接回的資料存到變數data
        var data = JSON.parse(this.responseText);
        
        // 6.~~ 應用data:  
            console.log(data);
    }
}
```
備註
1. ``.open('～',～, true/false)``
    - **`true` 非同步(預設值)**：程式碼**不會等資料回傳回來就會繼續執行後續程式碼**
    - **`false` 同步**：**等資料處理（回傳/接收）完畢才繼續往下執行後續程式碼**
    - 預設使用非同步的原因:若資料量大時等全部載完才執行後續動作UX很糟(卡在那)

2. `JSON.parse`
    - JSON格式資料型態是陣列內包物件
    - 資料傳輸時會被轉換成string(字串)
    - 使用JSON.parse將資料轉換回原本的格式（陣列包物件）

## 2. Axios:

### 示例

需先安裝Axios,引入CDN:
```html
<script src='https://cdnjs.cloudflare.com/ajax/libs/axios/0.19.2/axios.min.js'></script>
```

```javascript
var dataUrl= "https://cloud.culture.tw/frontsite/trans/SearchShowAction.do?method=doFindTypeJ&category=6"

axios.get(dataUrl)
.then( (res) => {
    console.log(res.data);
})
.catch( (err) => {
    console.log(err);
});
```

## 3. jQuery  $.Ajax()
### 示例
需先安裝jQuery,引入CDN:
```html
<script src='https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.min.js'></script>
```
    
```javascript
var dataUrl= "https://cloud.culture.tw/frontsite/trans/SearchShowAction.do?method=doFindTypeJ&category=6"
$.ajax({
    url: dataUrl,
    method: 'GET',
    dataType: 'json',
    data: '',
    async: true,　
   
    success: res =>{
        console.log(res)
        },
    error: err =>{
        console.log(err)
        },
});
```

### 詳解

```javascript
// 先把API的URL存成一個變數
var dataUrl= "API URL"
```
```javascript
$.ajax({
    url: dataUrl,  // 指定API 的 URL 
    method: 'GET', // 指定請求方法
    dataType: 'json',// API的格式
    data: '', //若有傳送資料時的資料設定 (GET沒有)
    async: true,　//  預設是true=非同步,false=同步 (true時整行可省略)
```
```javascript
    success: res =>{ // 成功的話執行...
        ...
        },
    error: err =>{ // 失敗的話執行...
        ...
        },
});
// 箭頭涵式寫法:success: res =>{  ....}
// 原始一般寫法:success: function(res){  ....}
```

## 參考文件

- 手冊
    - [MDN-XMLHttpRequest](https://developer.mozilla.org/zh-TW/docs/Web/API/XMLHttpRequest)
    - [axios](https://github.com/axios/axios)
- XMLHttpRequest
    - [練習使用簡單的 GET 方法接一個 open data](https://ithelp.ithome.com.tw/articles/10207897?sc=iThelpR)
- Axios
    - [純、手工系列 JS(Vue Axios篇)](https://ithelp.ithome.com.tw/articles/10194612)
- Ajax
    - [「使用網頁等公車」 ─ 從 AJAX 開始的 api 串接之旅](https://ithelp.ithome.com.tw/articles/10196742)
