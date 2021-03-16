---
title: '[jQuery] 實例-幻燈片圖片輪播切換-基本款(淡入淡出)'
tags: [JavaScript, jQuery]
category: jQuery
#   - - (所有文章)
#   - - 工程師－攻城路
#     - JavaScript
#     - Jquery
permalink: posts/26425
date: 2020-10-07 23:48:42
---

jQuery 基本圖片輪播切換效果。

<!--more--> 

---
# jQuery-實例 Slideshow

多張圖片切換的幻燈片效果

---

## Basic 基本款 定時淡入淡出

[>> CodePen Demo](https://codepen.io/eudora-hsj/pen/dyXyMdp)

<iframe height="500" style="width: 100%;" scrolling="no" title="*jQuery-Slideshow(basic)" src="https://codepen.io/eudora-hsj/embed/dyXyMdp?height=265&theme-id=light&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/eudora-hsj/pen/dyXyMdp'>*jQuery-Slideshow(basic)</a> by Eudora
  (<a href='https://codepen.io/eudora-hsj'>@eudora-hsj</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


#### HTML
```html
<div class="slideshow">
    <img src="https://picsum.photos/900/400?random=1" alt=""/>
    <img src="https://picsum.photos/900/400?random=2" alt=""/>
    <img src="https://picsum.photos/900/400?random=3" alt=""/>
    <img src="https://picsum.photos/900/400?random=4" alt=""/>
</div>
```


#### CSS
```CSS
.slideshow {
    position: relative;
    margin: auto;
    overflow: hidden;
    height: 400px;
    width: 900px;
}
.slideshow img {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    display: none;
}

```

#### JavaScript
```javascript
$('.slideshow').each(function(){
    
    let slideImgs = $(this).find('img'),
        slideImgsCount = slideImgs.length,
        currentIndex = 0;
    
    slideImgs.eq(currentIndex).fadeIn();
    
    setInterval(showNextSlide, 5000);
    
    function showNextSlide(){
        let nextIndex = (currentIndex + 1) % slideImgsCount;
        console.log(nextIndex)
        slideImgs.eq(currentIndex).fadeOut();
        slideImgs.eq(nextIndex).fadeIn();
        currentIndex = nextIndex;
    }
})
```

---

### 做法解析：

#### HTML

- 將總共要展示的所有圖片(img xN個)包在一個容器(div)中

    ```html
    <div class="slideshow">
        <img src=" ... ">
        ...
        <img src=" ... ">
    </div>
    ```

#### CSS
- 利用 absolute 的定位讓所有圖片重疊在一起

    ```CSS
    .slideshow {
        position: relative;
    }
    .slideshow img {
        position: absolute;
        top: 0;
    }
    ```

- 將所有圖片預設為隱藏(用jQuery控制顯示)
    ```CSS
    .slideshow img {
        display: none;
    }
    ```

#### JS

- 最外層選定$(父容器).each( ... ) 可使單頁面上的多組 slideshow 都生效 
 
    ```javascript
    $('.slideshow').each(function(){
        ...
    })
    ```

- （該單一組slideshow內）初始定義 3 個變數存放
    1. slideImgs：存所有 img 
    2. slideImgsCount：所有 img 數量
    3. currentIndex：當前要展示的圖在 slideImgs中對應的index值(第幾個):預設從第１張開始  
        （但JS中，取陣列內第"1"個的index值式"0"不是"1"，故這裡的變數定義初始值為 0 )  
          
    ```javascript
    let slideImgs = $(this).find('img'),
        slideImgsCount = slideImgs.length,
        currentIndex = 0;
    })
    ```
    
- 指定當前第Ｎ (currentIndex) 個img淡入方式顯示(`fadeIn()`)

    ```javascript
    slideImgs.eq(currentIndex).fadeIn();
    ```
- 使用 JS 原生的 [`setInterval()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setTimeout) 每隔固定的時間點重複執行指定的 function :觸發圖片轉換（當前的消失、下一張出現）
    ```javascript
    setInterval(showNextSlide, 5000)
    ```
    
- 定義圖片轉換的function：showNextSlide()
    ```javascript
    function showNextSlide(){
        let nextIndex = (currentIndex + 1) % slideImgsCount;
        slideImgs.eq(currentIndex).fadeOut();
        slideImgs.eq(nextIndex).fadeIn();
        currentIndex = nextIndex;
    }
    ```
    - 新定義一個變數存取「下一張圖片的 index值」：nextIndex（行２）
    - 範例中使用了四張圖片，依序「下一張」要被輪流展示的是第２、３、４、１、２……張，對應的 index 值是 １、２、３、０、１……
    - currentIndex　初始值為 0，統一 +1 後除圖片數量（slideImgsCount）取的餘數（`%`），指定給nextIndex
    - 選取當前圖片與下一張圖片，個別指定對應的淡出與淡入
    - 最後將 currentIndex　更新為 currentIndex，再進行下一回，就能讓 currentIndex 依序為 ０、１、２、３、０、１……

---

備註：
- [Lorem Picsum](https://picsum.photos/)  
範例中使用的圖片來自 Picsum，可快速生成指定比例的圖像

參考資料：
- 以上範例參考自[jQuery 達人的階梯](https://www.flag.com.tw/books/product/F4478)


---

⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10250594)

