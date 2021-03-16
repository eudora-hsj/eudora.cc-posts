---
title: '[CSS] Sass 新手入門(1)基本語法'
tags: [CSS, Sass]
category: 'CSS'
#   - - (所有文章)
#   - - 工程師－攻城路
#     - CSS

# banner_img: https://i.imgur.com/9Ew1COp.png
# index_img: https://i.imgur.com/9Ew1COp.png
# banner_mask_alpha: 0.5
# comments: true
permalink: posts/59814
date: 2020-09-26 06:08:10
---

簡介 CSS 預處理器 Sass 及基本語法。

<!--more--> 

---

<div class="fs-s mb-4r">

本文適用於...
- 已會使用 CSS 定義樣式（選用適當的選擇器定義屬性與屬性值）
- 已配置 Ssss 編譯 CSS 的開發環境（若還沒，[使用線上編輯器 CodePen](/posts/59814/#%E7%B7%9A%E4%B8%8A%E8%A9%A6%E8%A9%A6)來體驗一波）
- 想快速了解重點語法應用的 Sass 新手

</div>


![](https://i.imgur.com/9Ew1COp.png)
<!-- # [CSS] Sass 教學-新手上路重點摘要 -->

- Sass 是 **CSS Preprocessor**（**CSS 預處理器**）的一種
- 讓 CSS 設計過程能夠更加便利、有結構、更簡潔、更彈性
- 完成 SASS / SCSS 檔後**需編譯為 CSS 檔**

## **Sass 分兩種 - SASS & SCSS**

- SASS （Indented Sass）
    **不寫 { } 、不寫;**     
    **縮進取代{ }**，所以縮排相當重要、**不可空錯**
    **不兼容CSS**

    ```SCSS
    p
        color:black
        span
            color:red
    ```

- SCSS （Sassy CSS）
    一樣要寫{ }、;
    **兼容CSS**
    ```SCSS
    p{
        color:black;
        span{
            color:red;  
        }
    }
    ```



<div class="fs-s mt-2r">
以下先就以SCSS的特色寫法做整理
</div>

---

## 1. 巢狀結構
### 基本-選擇器(selector)
- 當CSS這樣寫時

    ```SCSS
    #banner{
        //...A
    }
    #banner #logo{
        //...Aa
    }
    #banner #logo img{
        //...Aa1
    }
    #banner nav{
        //...Ab
    }
    ```

    可用SASS以**巢狀**寫 (下例為SCSS)

    ```SCSS
    #banner{
        ...

        #logo{    // 等同於 #banner #logo
            ...

            img{  // 等同於 #banner #logo img
                ...
            }

        }

        nav{     // 等同於 #banner nav
            ... 
        }
    }
    ```
  

### & 連接
- 選擇器用**&符號接起父層**

    ```SCSS
    a{
        color:red; 
        &:hover{   //等同於　a:hover
            color:red;
        }
        
        &.active{  //等同於　a.active
            color:blue;
        }
    }
    ```
   
### CSS**屬性也可以巢狀**
- 常見前綴相同的屬性如 background / border / font...

    ```SCSS
    .box{
         background: {
            image: url(/img/bg.jpg);
            repeat: repeat;
            position: top;
        }
         font: {
             size: 1rem;     //等同於font-size:...
             weight: bold;   //     font-weight:...
        }
    }
  ```
  
 
---

## 2. 變數 $
### **$變數: 值**

- 例：色票管理

    ```SCSS
    $main-color: blue;
    $sub-color: gray;

    footer {
        background-color: $sub-color; 
        color: $main-color; 
    }
    p{
        color: $main-color; 
    }
    ```
  

- 變數內的值存數字／字串/布林/空/list/  
  map(key1:value,key2:value...)　都可以
 
 
---
 
## 3. `Mixin`
### 基本用法
1. **用`@mixin`定義**

    ```SCSS
    @mixin basic-space{
        padding: 1rem;
        margin: 1rem;
    }
    ```
2. **`@include` 引用** mixin

    ```SCSS
    .box{
        @include basic-space
    }
    ```
- 適用於管理重複性的設計定義(模組化管理的概念)

### 使用參數更彈性

1. `@mixin` 定義一個mixin**並帶入參數**

    ```SCSS
    @mixin basic-space($mg, $pd){
        padding: $mg;
        margin: $pd;
    }
    ```
2. `@include` 引用 mixin**並帶入參數**

    ```SCSS
    .wrap{
        @include basic-space(0, 1rem);
    }
    .box{
        @include basic-space(1rem,  0.5rem);
    }
    ```
- 讓不同selector直接以不同的屬性值去引用同一個mixin
    
    ![](https://i.imgur.com/12qL905.png)
 
---

## 4. 繼承 `@extend`
### 基本用法-定義

1. `%`開頭來定義一段開放被繼承的類

    ```SCSS
    %basic-space{
        padding: 1rem;
        margin: 1rem;
    }
    ```
2. 用 `@extend` 來繼承

    ```SCSS
    .wrap{
        @extend %basic-space;
        background-color: red;
        
    }
    .box{
        @extend %basic-space;
        font-size: 1rem;
    }
    .footer{
        @extend %basic-space;
    }
    ```
- selector 將自動被組合起來:

    ```SCSS
    .wrap, .box, .footer {
      padding: 1rem;
      margin: 1rem;
    }

    .wrap {
      background-color: red;
    }

    .box {
      font-size: 1rem;
    }
    ```


- **與mixin意義不同**:
    讓**多個selector(如A、B、C)都繼承同一段**stlye定義  
    編譯出來的CSS檔中該style定義**只會出現一段**  
    且為group selector**(A, B, C)** 

    
    ![](https://i.imgur.com/XCXhPPJ.png)

### **直接繼承某個 selector**
- 沒寫 % 預先定義、而是直接繼承於某個 selector

    ```SCSS
    .box {
        ...
    }

    .box-point {
        @extend .box;
        ...
    }
    ```

    
    ![](https://i.imgur.com/MCNcuco.png)


 
---

## 5. 運算符
- **基本加減乘除與變數運算**

    ```SCSS
    $box-width: 10rem ;

    .box {
        width: $box-width;
        img {
            width: $box-width / 2;
        }
    }	
    ```
    
    ![](https://i.imgur.com/W3KO02u.png)

- **有限制的跨單位計算**
    - [詳細參考大大文章](https://ithelp.ithome.com.tw/articles/10204038)
- 語法注意：**運算符（加減乘除）兩邊要有空格**

 
---

 
## 6. `@import` "_file"
- 透過**@import引入多個SCSS/SASS**
  
  使用情境例子：樣式依頁面或特殊需求**拆分成多個SCSS檔**，最後再統一**import到一個SCSS檔**，編譯時只編譯最終集成的這個SCSS檔**生成單一個CSS檔**（**減少 Request 檔案數**）*
    - 例如: 被拆分的數個CSS檔整合到 style.SCSS

    ```SCSS
    _reset.SCSS
    _layout.SCSS
    _product.SCSS
    _company.SCSS
    ```

    ```SCSS
    @import "reset"
    @import "layout"
    @import "product"
    @import "company"
    ```

        
    - 不打副檔名也OK，會自動抓同名的　　SASS檔或　SCSS　檔  
    - 只要監聽此檔即可,因**被引入的檔案會同時被監聽**
    - 編譯後的style.SCSS為被引入的所有檔的style
    - SCSS　/　SASS**檔名開頭為底線 _ 不編譯為CSS檔**
 
---


## 7. 註解與編譯
- 多行註釋　`/*  .... */`   會編譯到CSS檔內
- 以及單行註釋`/  ... /`   不會編譯到CSS檔內  
    
![](https://i.imgur.com/PpSnNYl.png)

---

## 線上試試
若你還沒安裝好 Sass 應用環境也可以先使用線上 Editor 來體驗一下
- 線上 Editor 如 [CodePen](https://codepen.io/)，設定參考:
  ![](/img-post/0718-1.gif)

- 或是將現有的CSS檔透過Converter感受一下簡化後的格式
  [CSS 2 SASS/SCSS CONVERTER](https://css2sass.herokuapp.com/)

---

## CSS / SASS / SCSS
- SCSS- 則較接近原始CSS的語法，擴充了巢狀、mixin、extend...等功能。
- SASS- 比 SCSS 更簡化到 {　} 跟 ; 都省略，相對縮排必須變得嚴謹。
    - 少了{  }符，有些人認為這樣反而很難閱讀。
    - 另一個缺點是無法像 SCSS 一樣通用原生 CSS ，若需複製一段 CSS Code 時（例如使用瀏覽器開發者工具進行試調後、套用框架的範本 code… 等），還需先進行轉換或自行刪除分號與括號。
- CSS Preprocessor 只是為了加速開發的一種應用，使用原生 CSS 或利用 Preprocessor 開發，就看個人與開發團隊的開發習慣囉！



---

## 參考資料
### SASSGuide
- [SASSGuide](https://SASS-lang.com/guide)
- [SASS中文網](https://www.SASS.hk/docs/)

### 其他文件

- [SASS教學 ＋SCSS：CSS再進化，掌握語法攻略！](https://frankknow.com/SASS-tutorial/)
- [SASS: 變數-運算單位](https://ithelp.ithome.com.tw/articles/10204038)

---

⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10244301)



