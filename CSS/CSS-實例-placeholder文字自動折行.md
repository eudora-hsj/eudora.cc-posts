---
title: '[CSS] 實例- placeholder 文字自動折行'
permalink: posts/815
date: 2020-12-02 23:12:00
tags: [CSS, placeholder, white-space]
category: 'CSS'
#   - - (所有文章)
#   - - 工程師－攻城路
#     - CSS
# comments: true

---

適用情境：input 輸入框內的placeholder提示文字太長，想自動折行。

<!--more--> 

---

<iframe height="300" style="width: 100%;" scrolling="no" title="CSS - input placeholder 自動折行" src="https://codepen.io/eudora-hsj/embed/wvGQGZx?height=265&theme-id=light&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/eudora-hsj/pen/wvGQGZx'>CSS - input placeholder 自動折行</a> by Eudora
  (<a href='https://codepen.io/eudora-hsj'>@eudora-hsj</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

```css
input {
  height: 2rem;
}
input::placeholder {
  transform: translateY(-0.5rem);
  white-space: normal;
}
```
---

重點:
1. 選擇器 `::placeholder`
2. `white-space: normal;`　超過容器寬度自動換行
3. `transform: translateY()`　偏移文字
   ![△未設定偏移時](https://i.imgur.com/VvnZbS1.png)

--- 
參考資料
- [CSS-white-space｜MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/white-space)
- [CSS-::placeholder｜MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/::placeholder)

<style>
img{
  box-shadow: none !important;
}
</style>