---
title: '[CSS] 動畫屬性 Animation 基本應用'
permalink: posts/10251496
date: 2020-10-09 06:07:10
tags: [CSS, Animation]
category: 'CSS'
#   - - (所有文章)
#   - - 工程師－攻城路
#     - CSS
# comments: true

---

關於 CSS Animation 屬性基本用法。

<!--more--> 

---

基本的樣式設定/ 排版定位 都已經難不倒你了嗎？那就接著要來玩玩動態的部分啦！一開始覺得寫 CSS 能讓醜醜的網頁變漂亮很療癒，而接觸了 CSS 的動畫控制，更是感到加倍療癒啊！  

本篇介紹最基本的語法：

---

## Animation 2 步驟 起手式

### step1. 定義動畫: `@keyframes`  

```css
@keyframes 動畫名稱{
    from{
        opacity:0.5;
    }
    to{
        opacity:1;;
    }
}
```
- 給這個動畫一個名稱　`@keyframes 動畫名`
- 裡面的每一段為「關鍵影格」。
- 除了 `from` 、 `to`，還能用百分比來定義
    ```css
    @keyframes 動畫名稱{
        0%{
            ...
        }
        50%{
            ...
        }
        100%{
            ...
        }
    }
    ```
    小細節：  
    - 百分比的意思是，在整個動畫時間長度內的百分之幾的位置設下關鍵影格，所以不會有120%這種數字出現欸！
    - 通常會定義清楚0%、100%，如果沒有定義頭跟尾，會被程式自動腦補，有可能跟你預期的不同！故通常起訖會定義。
    - 如果重複指定相同的關鍵影格會怎樣？
        ```css
        50%{
            ...
        }
        50%{
            ...
        }
        ```
        - 相同屬性時：後面會覆蓋前面
        - 屬性不相同時，都能正常生效。
    - 如果我定義了兩段相同動畫名稱的動畫，會怎樣？ 
        - 同css權重後面蓋前面的概念，前面的會被後面的動畫給蓋掉


### Step2. 將指定的元素掛上動畫:

```css
selector{
    animation-name: 動畫名稱;
    animation-duration:2s;
}
```

---

### 範例

- [Codepen 栗子](https://codepen.io/eudora-hsj/pen/Bazyxp)

    ```css
    @keyframes move{
        from{
            opacity:0;
            left: 0;
            background: orange;
        }
        to{
            opacity:1;
            left: 100px;
            background: blue;
        }
    }

    .box{
        animation-name: move;
        animation-duration:2s;
        ...(略)
    }    
    ```

![](https://eudora.cc/img-post/1009-2.gif)


最最最基本的寫法，這樣就可以動囉！  

範例中關鍵影格使用了不同的顏色屬性，來看看自動生成的顏色：  
![](https://i.imgur.com/lrTk8gk.png)  

這漸層真美啊!  

---

## 其他的屬性定義：  

1. `animation-duration: 持續時間`
2. `animation-delay: 延遲播放時間`
3. `animation-timing-function: 轉場(補間方式)效果函式`

類似 `Transition` 轉場動畫的基本屬性:

1. `transition-duration: 持續時間`
2. `transition-delay: 延遲播放時間`
3. `transition-timing-function: 轉場(補間方式)效果函式`

而 transition 的 `transition-property: 屬姓名` (要生效的屬性) 就相當於 animation 的 `animation-name: 動畫名`  (要生效的動畫) 的角色。

除了上述跟 transition 類似的屬性外，還有以下：

- `animation-iteration-count: 數字` 指定動畫重複執行次數
    - 數字（次數）
    - `:infinite` 無限循環

- `animation-direction:` 指定動畫方向
    - `: reverse` 逆向  
    - `: alternate` :頭尾相接：隨播放次數正向→反向→正向→反向→…


![](https://eudora.cc/img-post/1009-3.gif)
![](https://eudora.cc/img-post/1009-2.gif) 



---

開啟 Codepen 來玩看看吧!

- [Codepen 栗子](https://codepen.io/eudora-hsj/pen/dyXPjPp)

<!-- ![](https://eudora.cc/img-post/1009-3.gif) -->


---

⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10251496)



