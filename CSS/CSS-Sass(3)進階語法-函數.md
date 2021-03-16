---
title:  '[CSS] Sass 新手入門(3)函數應用'
date: 2020-09-26 04:08:10
tags: [CSS, Sass]
category: 'CSS'
#   - - (所有文章)
#   - - 工程師－攻城路
#     - CSS
permalink: posts/31491

---
續[上一篇](https://eudora.cc/posts/31495/) Sass 進階應用，這篇列表 Sass 內建函數，及自定義函數的用法。

<!--more--> 


---

## 內建函數

#### lighten & darken

- 基本語法
    ```scss
    :lighten( color, 50%)
    :darken( color, 50%)
    ```

- 範例
    ```scss
    $color-main: #00F;
    $color-main-light30: lighten($color-main, 30%);
    $color-main-dark30: darken($color-main, 30%);

    a{
        background-color: $color-main;
        &:hover{
            color: $color-main-light30;
        }
        &:active{
            color: $color-main-dark30;
        }
    }
    ```

    ![](https://i.imgur.com/1NwPHrq.png)

---

#### 補充：關於hsl & hsla

*一般網頁色瑪用 RGB(#00FF00)來定義，六個數字兩兩一組各代表紅色、綠色、藍色的色值，而色值是16進位制表示0~255之間(00 = 0，FF = 255）*


- hsla:
    - 色相（Hue）: 0~360
    - 飽和度（Saturation）: 0 ~ 100%
    - 亮度（Lightness）: 0 ~ 100%
    - 透明度（alpha）: 0 ~ 1



- 基本語法
    ```scss
    hsl(0, 100%, 50%)
    hsla(0, 100%, 50%,　0.5 )
    ```
    
- 範例

    ```scss
    span{
        color: hsl(20, 100%, 50%);
        background-color: hsla(20, 100%, 50%, 0.5);
    }

    ```

    ![](https://i.imgur.com/AhYPiSv.png)
    
---


### 顏色函數

 | function       | do  | eg         |
 | :----------- | :--- | :--------- | 
|	`adjust-hue(color, __deg)`	|	調整顏色的色相(hsl中的h)	|	($main-color, 137deg)	|
|	`saturate(color, __%)`	|	增加顏色的飽和度(hsl中的S)	|	($main-color, 50%)			|
|	`desaturate(color, __%)`	|	減少顏色的飽和度(hsl中的S)	|	($main-color, 50%)			|
|	`transparentize(color, 0.3)`	|	顏色變得更透明<br/>(減少alpha值)	|	($main-color, 0.3)		<br/>原本alpha-0.3	|
|	`opacify(color, 0._)`	|	顏色變得更不透明<br/>(增加alpha值)	|	($main-color, 0.3%)		<br/>原本alpha+0.3	|
|	`lighten(color, __%)`	|	增加顏色亮度(明度)	|	($main-color, 30%)			|
|	`darken(color, __%)`	|	減少顏色亮度(明度)	|	($main-color, 30%)			|

### 數字函數


 | function       | do  | eg         | 
 | :----------- | :--- | :--------- | 
|	`abs()`	|	絕對值	|	(-5)→5	|
|	`round()`	|	取整數-四捨五入	|	(-3.6)→4<br/>(-3.1)→3	|
|	`ceil()`	|	取整數-無條件進位	|	(-3.6)→4<br/>(-3.1)→4	|
|	`floor()`	|	取整數-無條件捨去	|	(-3.6)→3<br/>(-3.1)→3	|
|	`percemtage()`	|	計算比例	|	(10px / 100px)  → 10%	|
|	`min()`	|	取最小值	|	(1, 2, 3)  → 1	|
|	`max()`	|	取最大值	|	(1, 2, 3)  → 3	|


### 文字函數


 | function       | do  | eg         | 
 | :----------- | :--- | :--------- | 
|	to-upper-case()	|	字串轉大寫	|	(Hello)→HELLO	|
|	to-lower-case()	|	四捨五入取整數	|	(Hello)→hello	|
|	str-length()	|	回傳字串長度	|	(Hello)→5	|
|	str-index(string, keyword) <br/>(index從1開始)	|	查特定自在字串中的位置	|	("Hello Eudora", "Hello")→1	|
|	str-insert(string, addString, index)	|	字串中插入值	|	("Hello", " Eudora", 5)→"Hello Eudora"	|

## 自定義函數

- 語法
    ```sass
    @function name(argument1, argument2...){
        ...
        @return ...
    }
    ```
- 例：搭配 map 應用
    ```sass
    $theme: (
        light: #ccc,
        dark: #222
    );

    @function theme($mode) {
        @return map-get($theme, $mode);
    }

    body {
        background-color: theme(dark);
    }
    ```
    compiled:
    ```css
    body {
        background-color: #222;
    }
    ```
---

參考資料
- [顏色空間(HSV/HSB與HLS)的區別|ITREAD01.COM](https://www.itread01.com/content/1546155122.html)
- [Sass @function](https://sass-lang.com/documentation/at-rules/function)
- [《 Sass 基础 》 - 宁皓网](https://ninghao.net/video/2133)
    
---
