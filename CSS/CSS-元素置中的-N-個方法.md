---
title: '[CSS] 元素置中的 N 個方法'
tags: [CSS, position, display]
# comments: true
category: CSS
#   - - (所有文章)
#   - - 工程師－攻城路
#     - CSS
permalink: posts/31492
date: 2020-09-24 11:50:13
---

元素置中是調控 CSS 時必然會遇到的問題，也是 Junior 前端工程師面試的熱門考題。這篇列出常見的置中方式。

<!--more--> 

---

定義限制條件：

1. 讓子元素水平、垂直皆居中：
    ![](https://i.imgur.com/dHFenW1.png)  
2. 置中的設定不能寫死特定的偏移值  
　(當父／子元素的寬高有變化時仍要維持居中)
ps. 下列範例以 以兩個 div 父（.container)子(.box)結構為例


```HTML
<div class="container">
    <div class="box">
    </div>
</div>
```




---



## 寫法1：Flex 標配置中屬性

```css
.container{
    display: flex;
    justify-content: center; 
    align-items: center; 
}
```
[> Codepen Demo](https://codepen.io/eudora-hsj/pen/zYqdabK)  

1. 將父層設為 display： flex
2. 定義 Flex 子物件  
   - `justify-content：center` 　主軸對齊方式：居中   
   - `align-items:center`  　次軸對齊方式：居中

---

## 寫法２：Flex + Margin auto

```css
.container{
    display: flex;
    
    .box{
        margin: auto
    }
}
```

[> Codepen Demo](https://codepen.io/eudora-hsj/pen/BaKxgWL)  

- `margin: auto`：將剩餘空間自動分配  
- `display` 設為  `grid` / `inline-flex` / `inline-grid` 定義完整空間。


---

## 寫法3：Absolute + TRBL 0 + Margin auto
```css
.container{
    position: relative; 
    
    .box{
        position: absolute; 
        top: 0;             
        bottom: 0;           
        left: 0;        
        right: 0;
        margin: auto;      
    }
}
```
[> Codepen Demo](https://codepen.io/eudora-hsj/pen/BaKdVrO)  

- `position: absolute` 指定 `top` / `right` / `bottom` / `left`　時是以「第一個有定位的父層容器」為位移基準。  
- 有定位是指 `position` 為 `relative` / `absolute` / `fixed`  
   - 若想指定為對整依據的父層但原先沒有特別指定 position　又不想影響到該排版，可直接指定為 `relative`，因為 relative 在未指定 `top` / `right` / `bottom` / `left` 時不會有任何改變。
   - 如果所有父層都沒有定位，則將對齊「視窗」
-  將 `top` / `right` / `bottom` / `left` 指定為 `0` 時，會自動計算為可運用的空間。
- `margin: auto`：將剩餘空間做自動分配
- 注意：此方法只適用於定位物件要有明確寬度與高度！


---


## 寫法４：Absolute +  LT  50% +Translate  -50%

```css
.container{
    position: relative;
    
    .box{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
    }
}
```

[> Codepen Demo](https://codepen.io/eudora-hsj/pen/ZEWoRqJ)  

- 類似方法 3
- `position: absolute` 依據其「有定位的父層」做位移。
- `top: 50%`、`left: 50%` 進行向下、左位移 50%：
- 但因物件對齊點為左上角，故須進行 X、Y 軸負向偏移 50% 讓對齊點為物件中心：`transform: translate(-50%,-50%)`　才可真正置中。

---



## 寫法５：Relative +  LT  50% +Translate  -50%

```css
.container{
    
    .box{
        position: relative;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%)
    }
}
```

[> Codepen Demo](https://codepen.io/eudora-hsj/pen/XWdqLex)  

- 類似做法4。  
- `position: relative` 指定 `top` / `right` / `bottom` / `left`　時為原本位置做偏移。  

---


##  寫法６：偽元素 + inline-block +  vertical-align + text-align

```css
.container{
    text-align: center;
    font-size: 0;
    
    &:after{
        content: '';
        height: 100%;
        vertical-align: middle;
        display: inline-block;
        width: 0px;
    }
    
    .box{
        display: inline-block;
        vertical-align: middle;
        
    }
}
```

[> Codepen Demo](https://codepen.io/eudora-hsj/pen/poyVXBZ)  



---

## 參考文件
- [連續30天的超實務網頁設計的垂直置中教學／Amos](https://ithelp.ithome.com.tw/users/20112550/ironman/2092)
- [23種CSS垂直置中技巧／Amos](http://csscoke.com/2018/08/21/css-vertical-align/)
- [CSS 垂直置中的七個方法／oxxo](https://www.oxxostudio.tw/articles/201502/css-vertical-align-7methods.html)
- [CSS 垂直置中的三個方法／oxxo](https://www.oxxostudio.tw/articles/201408/css-vertical-align.html)
- [探秘 flex 上下文中神奇的自動 margin](https://kknews.cc/zh-tw/code/pl88x5p.html)

---

⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10243438)


