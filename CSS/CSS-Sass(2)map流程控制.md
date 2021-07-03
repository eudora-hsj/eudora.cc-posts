---
title:  '[CSS] Sass 新手入門(2)-變數、Map、流程控制指令'
date: 2020-09-26 05:08:10
tags: [CSS, Sass]
category: 'CSS'
#   - - (所有文章)
#   - - 工程師－攻城路
#     - CSS
permalink: posts/31495

---
續[上一篇](/posts/59814/) Sass 基本的語法應用，這篇來介紹 Sass 的進階語法，讓你會一度有 CSS 是程式語言的錯覺。

<!--more--> 

---


## 變數

- 定義變數variable　`$variable:__  `
- 插值(插入變數)　``#{variable}``


## Map


- 基本語法
    ```SCSS
    $variable: (
        key: value,
        key: value
    );
    ```


- 範例

    ```scss
    $z-index: (
        container: 5,
        header: 10,
        notice: 20
    );

    .header{
        z-index: map-get($z-index, header);
    }
    .container{
        z-index: map-get($z-index, container);
    }
    .notice{
        z-index: map-get($z-index, notice);
    }
    ```

   ![](https://i.imgur.com/omsZfC7.png)



---

## 控制指令 Control Directives

1. `@if`
2. `@for`
3. `@each`
4. `@while`

---

## @if

- 基本語法
    ```scss
    @if{

    }
    ```

- 範例
    ```scss
    $theme: "dark";

    body{
        @if $theme == dark {
            background-color: black
        }@else if  $theme == light {
            background-color: white
        }@else{
            background-color: grey;
        } ;
    }
    ```

    ![](https://i.imgur.com/OG81mmJ.png)

---


## @for

- 基本語法(1) to 不包含結束值
    ```scss
    @for $var from 起始值 to 結束值{

    }
    ```


- 範例
    ```scss

    $cols: 4;

    @for $col from 1 to $cols{   
        .col-#{$col}{                
            width: 100% / $cols * $col; 
        }
    }

    ```

    ![](https://i.imgur.com/cwRgSBL.png)



- 基本語法 (2) through 包含結束值
    ```scss
    @for $var from 起始值 through 結束值{

    }
    ```


- 範例
    ```scss

    $cols: 4;

    @for $col from 1 through $cols{  
        .col-#{$col}{                
            width: 100% / $cols * $col; 
                                      
        }
    }

    ```
    
    ![](https://i.imgur.com/YfayfLP.png)
    
    
那之前純手刻還拿出計算機計算的 12 欄網格系統



```scss

.col-1 {
    width: 8.33333%; }

.col-2 {
    width: 16.66667%; }

.col-3 {
    width: 25%; }

.col-4 {
    width: 33.33333%; }

.col-5 {
    width: 41.66667%; }

.col-6 {
    width: 50%; }

.col-7 {
    width: 58.33333%; }

.col-8 {
    width: 66.66667%; }

.col-9 {
    width: 75%; }

.col-10 {
    width: 83.33333%; }

.col-11 {
    width: 91.66667%; }

.col-12 {
    width: 100%; }

```

在 sass 只要這樣呢！

```scss
$cols: 12;

@for $col from 1 through $cols{   
    .col-#{$col}{                 
        width: 100% / $cols * $col; 
    }
}
```

這實在是……太太太太太療癒啦！


---

## @each


- 基本語法
    ```scss
    @each $___  in $___s {
    
    }
    ```

- 範例
    ```scss
    $status: sucess error warning;

    @each $statu in $status {
      .icon-#{$statu} {
        background-image: url('img/icons/#{$statu}');
      }
    }
    ```

    ![](https://i.imgur.com/1gNWWW5.png)

  
---

## @while


- 基本語法
    ```scss
    @while _____ { 
    
    }
    ```

- 範例
    ```scss
    $num: 8;

    @while $num > 0 {
      .w-#{$num} {
        width: 10px * $num;
      }

      $num: $num - 2; 
    }
    ```

    ![](https://i.imgur.com/m8CimEh.png)


---


是否有點認不出 CSS 了呢 XD？以上範例為了凸顯單項語法重點，沒綜合應用其他語法，例如可觀察到範例中有一些類似的、重複的語句，可以應用於前一篇提到的 mixin ...等技巧，同時應用，使得 SCSS 更為精簡!

    
---

參考資料
- [Sass教學-使用Sass Maps|廖洧杰](https://ithelp.ithome.com.tw/articles/10161389)
- [SASS : SASS Maps|yuski](https://ithelp.ithome.com.tw/articles/10207093)
- [Sass基礎》》-寧皓網](https://ninghao.net/video/2128)
- [Sass教程網](https://www.sass.hk/docs/)

    
---

⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10245392)



