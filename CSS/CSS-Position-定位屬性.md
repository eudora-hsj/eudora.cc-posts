---
title: '[CSS] 定位屬性 Position'
date: 2020-09-28 19:51:41
tags: [CSS, Position]
category: 'CSS'
#   - - (所有文章)
#   - - 工程師－攻城路
#     - CSS
permalink: posts/31496

---

還記得剛學 CSS 的時後老是搞不清楚 position ，每次都盲試。定位是學 CSS 必定要搞清楚的基本功，理清楚各個屬性值的原理及特性才可以隨心所欲的駕馭自如哦～　

<!--more--> 

---

## inline / block

1. 單行元素－inline
    - 只算長度（資料長度）、沒有面積
    - 實際占用的高度就是資料本身的高度、不是被指定的高度
    - 寬度(width)、高度(height)設定無效
    
2. 塊狀元素－block
    - 能夠指定寬度(width)、高度(height)
    
3. inline-block => 有著 block 可指定寬高的特性，但又同 inline 與別物件置於同一列。

- 細節差異:

| attr                 | inline         | block        | inline-block   |
| -------------------- | -------------- | ------------ |:-------------- |
| width & height       | X              | O            | O              |
| padding top / bottom | X              | O            | O              |
| padding left / right | O              | O            | O              |
| margin top / bottom  | X              | O            | O              |
| margin left / right  | O              | O            | O              |
| 預設排列方式         | 與其他物件同列 | 自己佔據一列 | 與其他物件同列|

---


## Postition
1. `static`：靜態 (預設值)
3. `relative`：相對定位
4. `absolute`：絕對定位
5. `fixed`：固定
6. `sticky`：黏貼



### TRBL：`top` / `right` / `bottom` / `left`
- `top`:自定位基準上緣向下偏移
- `right`:自定位基準右緣向左偏移
- `bottom`:自定位基準下緣向上偏移
- `left`:自定位基準左緣向右偏移


---


### `position: static`
- 為未定義 `position` 時的預設值
- 定義 `TRBL` 屬性無效
- 處於原本的資料流


---


### `position: relative`
- 初始位置(0,0)以原本的位置為基準做`TRBL`偏移，仍佔據初始位置空間
- 若未設定偏移值`TRBL`時，位置不會變
    -> 故若需作為「有定位的父層」而不想做任何位移時，可設為 relative 而不指定TBRL
- 來看栗子：就原地偏移[>> Codepen](https://codepen.io/eudora-hsj/pen/NWNmgaa?editors=1100)

    
    ```css
    .box {   
        position: relative;
        left: 10px;
        top: 20px;
    }
    ```


![](https://i.imgur.com/aI1uJAw.png)


---



### `position: absolute`
- 物件抽離(獨立1層)，不佔據初始位置空間
- 初始位置(0,0)以「有定位的父層」為基準
    - 「有定位」指的是 position 為 fixed / absolute  / relative / sticky
    - 若都無定位時最頂層，則為視窗（windows）


- 來看栗子：就父容器為基準偏移[>> Codepen](https://codepen.io/eudora-hsj/pen/wvGZeEP?editors=1100)

    ```css
    .container .box {   
        position: absolute;
        left: 10px;
        top: 20px;
    }
    
    .container{
        position: relative;
    }
    ```
    
    ![](https://i.imgur.com/CPloTU5.png)
    

 - 相較於 relative ，偏移起點是有定位的父容器，且原始位置的空間不會佔據!

---



### `position: fixed`
- 物件抽離(獨立1層)，釋出初始位置空間（不佔原始空間）
- 初始位置(0,0)以「視窗 (window)」為基準
- 高、寬度沒指定時，會以內容撐開。
- 父層的寬高 / margin 失效
- 如果初始位置本來就超過視窗高度、又沒有指定TRBL時，會形同隱藏(怎麼捲都看不到)
- 觀察栗子：黑屏+彈出小視窗[>> Codepen](https://codepen.io/eudora-hsj/pen/XWdQppy?editors=1100)
    
    ```css
    .box {    
        position: fixed;
        left: 0;
        top: 0;
        right: 0;
        bottom: 0;
        margin: auto;
    }
    ```
    ![](https://i.imgur.com/iFTl4Lj.png)

---

### `position: sticky` 黏貼
- 基於當前滾動位置定位
- 捲出前特性為 position: relative;、捲出畫面時特性為 position: fixed;
- 觀察栗子：捲動時置頂/置底 [>> Codepen](https://codepen.io/eudora-hsj/pen/PoNgbjM)
    
    ```css
    .title {
        position: sticky;
        top: 0;
    }
    ```
    
    ![](https://eudora.cc/img-post/0929.gif)
    
    當然你也可以同時指定 bottom: 0，則不管往上或往下捲，物件都會恆在。
    
    ```css
    .title {
        position: sticky;
        top: 0;
        bottom: 0; 
    }
    ```
    
    ![](https://eudora.cc/img-post/0929-2.gif)
    
 
---

## z-index

當你觀察到了 fixed、absolute 有「抽出來獨立一層」的空間概念後，並且交叉運用後，就容易遇到預期之外的覆蓋問題，例如預期物件公告訊息彈出小視窗要保持最上層，卻被設計為捲動時維持畫面上方的 header 給遮住，這時要使用 z-index 指定彼此的層級關係(數字越大越上面)。

---


參考資料
- [ASTRO X 五倍紅寶石 全端工程師實戰訓練營 | Amos](https://astro.5xruby.tw/)
- [前端新手村 Position 定位](https://ithelp.ithome.com.tw/articles/10194075)

---


⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10245661)
