---
title: '[Vue.js] 實例-SlidesShow 圖片輪播切換'
tags: [JavaScript, Vue.js]
category: Vue.js
date: 2021-03-25 11:46:42
permalink: posts/210325

---

示例 常見的圖片輪播效果

<!--more--> 

> 適用:
> - 略知 Vue.js 結構(monted/data/methods)
> - 略知 Vue.js 的 transition 用法
> - 略知 JavaSciprt 的 setInterval
  
---

## Demo
<iframe height="600" style="width: 100%;" scrolling="no" title="Vue.js-Slideshow" src="https://codepen.io/eudora-hsj/embed/NWdGoxr?height=265&theme-id=dark&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/eudora-hsj/pen/NWdGoxr'>Vue.js-Slideshow</a> by Eudora
  (<a href='https://codepen.io/eudora-hsj'>@eudora-hsj</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---

##　重點：

   1. 上一頁
   2. 下一頁
   3. 指定特定頁
   4. 定時自動播放(下一頁)
   5. 最末頁再跳下一頁時,返回第一頁;
      第一頁再跳前一頁時,返回最末頁
   6. 過場動畫有順向與反向

---

<!--
## Code 
-->


### Template

```html
    <div id="app">
        <div class="slides">
            <transition-group tag="div" :name="transitionName" class="img-boxex" >
                <div v-for="(img, idx) of imgs" :key="idx" 
                     class="img-box" v-show="idx === showImg">
                    <img :src="img.src" />
                    <span>{{ idx + 1 }}</span>
                </div>
            </transition-group>
            <div class="btn-group">
                <button class="prev" @click="setShowImg(-1)">◀</button>
                <button class="page" @click="setShowImgTo(num - 1)" 
                        v-for="num in imgs.length" :key="num - 1" >{{ num }}</button>
                <button class="next" @click="setShowImg(1)">▶</button>
            </div>
        </div>
    </div>
</template>
```

### SCSS (只擷取主要)

```css
.slides {
    margin: auto;
}
.img-boxex {
    position: relative;
    width: 600px;
    height: 400px;
    overflow: hidden;
    margin: 20px auto;
}
.img-box {
    position: absolute;
}

.right-in-enter {             
    left: 100%;
}
.right-in-enter-active,      
.right-in-leave-active {     
    transition: left 0.5s;
}
.right-in-enter-to,          
.right-in-leave {           
    left: 0%;
}
.right-in-leave-to {        
    left: -100%;
}

.left-in-enter {            
    right: 100%;
}
.left-in-enter-active,      
.left-in-leave-active {    
    transition: right 0.5s;
}
.left-in-enter-to,
.left-in-leave {
    right: 0%;
}
.left-in-leave-to {
    right: -100%;
}
```

### script

```javascript

data() {
    return {
        transitionName: "right-in",
        showImg: 0,
        imgsCount: 8,
        imgs: [
            { src: "https://picsum.photos/600/400?random=1" },
            { src: "https://picsum.photos/600/400?random=2" },
            { src: "https://picsum.photos/600/400?random=3" },
            { src: "https://picsum.photos/600/400?random=4" },
            { src: "https://picsum.photos/600/400?random=5" }
        ]
    };
},
mounted() {
    setInterval(this.setShowImg, autoPlayInterval);
},
methods: {
    setShowImg(changeIdx = 1) {
        switch (true) {
            case changeIdx === 1 && this.showImg === this.imgs.length - 1:
                this.showImg = 0;
                break;
            case changeIdx === -1 && this.showImg === 0:
                this.showImg = this.imgs.length - 1;
                break;
            default:
                this.showImg = this.showImg + changeIdx;
                break;
        }
    },
    setShowImgTo(changeIdxTo) {
        this.showImg = changeIdxTo;
    }
},
watch: {
    showImg(nIdx, oIdx) {
        this.transitionName = nIdx > oIdx ? "right-in" : "left-in";
    }
}
```

<!--

## 說明

---

-->

---

[> CodePen]([https://codepen.io/eudora-hsj/pen/NWdGoxr])

<iframe height="500" style="width: 100%;" scrolling="no" title="Vue.js-Slideshow" src="https://codepen.io/eudora-hsj/embed/NWdGoxr?height=265&theme-id=dark&default-tab=js" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/eudora-hsj/pen/NWdGoxr'>Vue.js-Slideshow</a> by Eudora
  (<a href='https://codepen.io/eudora-hsj'>@eudora-hsj</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



---

## 參考資料
   - [[ 一個範例玩轉 Vue ] #3 簡易輪播功能與進退場](https://www.youtube.com/watch?v=VjFexIwgcgw&t=200s)
   - [Vue中使用定时器setInterval和setTimeout](https://www.cnblogs.com/jin-zhe/p/10001236.html)