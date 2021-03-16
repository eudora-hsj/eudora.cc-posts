---
title: '[CSS] 實例-文字漸層色'
permalink: posts/810
date: 2020-12-01 23:12:00
tags: [CSS, linear-gradient, text]
category: 'CSS'
#   - - (所有文章)
#   - - 工程師－攻城路
#     - CSS
# comments: true

---

用css將文字套用漸層顏色。

<!--more--> 

---

<iframe height="150" style="width: 100%;" scrolling="no" title="[CSS] 文字顏色漸層" src="https://codepen.io/eudora-hsj/embed/dyXjvEq?height=265&theme-id=light&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/eudora-hsj/pen/dyXjvEq'>[CSS] 文字顏色漸層</a> by Eudora
  (<a href='https://codepen.io/eudora-hsj'>@eudora-hsj</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

```css
h1{
  background: linear-gradient(to top, #3a1c71, #d76d77, #ffaf7b);
  background: -webkit-linear-gradient(to top, #3a1c71, #d76d77, #ffaf7b);
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}
```
---

原理:
1. 設定漸層背景 `background: linear-gradient(~~);`
   ![](https://i.imgur.com/4ykeIlj.png)
2. 設定背景裁切模式為文字 `background-clip: text;`
   ![](https://i.imgur.com/5DMaknW.png)
3. 將文字顏色指定為透明 `color: transparent;`
   ![](https://i.imgur.com/MvkFfeV.png)

--- 
參考資料
- [background-clip 背景裁切效果與漸層文字｜鬍子喬治](https://blog.george-moustache.com/background-clip-%E8%83%8C%E6%99%AF%E8%A3%81%E5%88%87%E6%95%88%E6%9E%9C%E8%88%87%E6%BC%B8%E5%B1%A4%E6%96%87%E5%AD%97/)

<style>
img{
  box-shadow: none !important;
}
</style>