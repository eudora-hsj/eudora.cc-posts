---
title: '[CSS] 語法-選擇器'
permalink: posts/809
date: 2020-09-23 06:07:10
tags: [CSS, Selector]
category: 'CSS'
#   - - (所有文章)
#   - - 工程師－攻城路
#     - CSS
# comments: true

---

本篇列表常見 CSS 選擇器、並以自己理解的方式去重新筆記。
<!--more--> 
---

熟練 CSS 選擇器的各種花式(?)運用可以大幅減少你對元素定義 class / id 值，也可以輕易地實踐設計師各種(~~龜毛~~)精緻的樣式要求。  
例如動態生成的數筆資料，設計圖指定要單、雙行不同樣式，或是從第 N 個開始每 N 個樣式突出……等，千萬不要用 JS 去掛指定的 class name　啊！能 CSS 解決的就不寫 JS！  

在看選擇器之前，先來看一下 CSS 的語法結構-三件事情、三個關鍵名詞：
![](https://i.imgur.com/BFyhny0.png)

選擇器就是你指定「網頁上的哪些元素」起來做樣式定義。所以你也可以把「選擇器」的語法理解為「取網頁上特定元素的篩選條件。」

---

## 依元素、名 (class / id)
| Syntax |Mean  | Selector |     
| :-------- | :-------- | :-------- | 
|	`el`	|	以 html tag選取	|	p	|
|	`.` class	|	class 值為___的元素	|	.active	|
|	`#` id	|	id 值為___的元素	|	#slider	|
|	`*`	|	所有元素	|		|

◎ class & id 命名規則：
1. 首字不可為數字(可以使用中線、底線)
2. 大小寫視為不同


---

## 依父子 / 同輩關聯
| Syntax |Mean  | Selector |     
| :-------- | :-------- | :-------- | 
|	elA`,` elA	|	A 跟 B	|	h1, h2	|
|	elA`  `elB	|	A 裡的所有 B (含子層 / 子子層 ...)	|	p span	|
|	elA `>` elB	|	A 的下一子層 的所有 B (不含子子層)	|	article > h2	|
|	elA `+` elB	|	緊接在 A 後面的 B (同輩)	|	h1 + p	|
|	elA `~` elB	|	接 A 後面的所有 B（同輩）|	h1 ~ p	|

---

## 依屬性與屬性值
| Syntax |Mean  | Selector |     
| :-------- | :-------- | :-------- | 
|	X`[ attr ]`	|	有特定屬性的元素	|	[target]	|
|	X`[ attr = val ]`	|	有___屬性且屬性值為___的 X	|	a[target=_blank]	|
|	X`[ attr ~= val ]`	|	有___屬性且屬性值"包含"為___的 X	|	article[data-type~="news"]	|
|	X`[ attr ^= val ]`	|	有___屬性且屬性值"開頭"為___的 X	|	a[src^="https"]	|
|	X`[ attr $= val ]`	|	有___屬性且屬性值為___"結尾"的X	|	a[src$=".pdf"]	|
|	X`[ attr *= val ]`	|	有___屬性且屬性值"包含"___的X	|	img[src*="index"]	|

---

## 偽類
| Syntax |Mean  | Selector |     
| :-------- | :-------- | :-------- | 
|	`:link`	|	連結預設樣式	|	a:link	|
|	`:visited`	|	已點過的連結	|	a:visited	|
|	`:hover`	|	游標移到Ｘ時	|	button:hover	|
|	`:active`	|	點擊當下(按下去到放開之間)	|	a:active	|
|	`:focus`	|	X focus 狀態	|	input:focus	|

◎ `<a>`四種偽類建議定義順序(避免衝突):
 1. `a:link`
 2. `a:visited`
 3. `a:hover`
 4. `a:active`

---

## 偽元素
| Syntax |Mean  | Selector |     
| :-------- | :-------- | :-------- | 
|	X` ::before`	|	在 X 的內容最前面插入內容	|	article:before	|
|	X` ::after`	|	在 X 的內容最後面插入內容	|	article:after	|


◎ 其預設 display 屬性為 `inline-block`  
◎ 一定要指定 `content` 屬性才會作用，不想放內文可設為空 `content: ''`

---

## 偽元素－首行/首字/被選中的
| Syntax |Mean  | Selector |     
| :-------- | :-------- | :-------- | 
|	X`::first-letter`	|	X 裡第一個字母	|	p:first-letter	|
|	X`::first-line`	|	X 裡第一行	|	p:first-line	|
|	X`::selection`	|	被 user 選取的元素	|		

◎ [關於`::selection`｜MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::selection)

---

## 子元素歷遍
| Syntax |Mean  | Selector |     
| :-------- | :-------- | :-------- | 
|	Ｘ`:first-child`	|	同層(其父元素的子層)裡的第一個元素且為Ｘ	|	p:first-child	|
|	Ｘ`:last-child`	|	同層(~)裡的最後一個元素且為Ｘ	|	p:last-child	|
|	Ｘ`:nth-last-child(n)`	|	同層(~)裡的倒數第 N 個、且為Ｘ	|	p:nth-last-child(2)	|
|	Ｘ`:nth-child( n )`	|	同層(~)裡的第 N 個且為Ｘ	|	p:nth-child(2)	|
|	Ｘ`:nth-child( 2n )`	|	同層(~)裡的第偶數個、且為Ｘ	|	p:nth-child(2n)	|
|	Ｘ`:nth-child( 2n+1 )`	|	同層(~)裡的第奇數個、且為Ｘ	|	p:nth-child(2n+1)	|
|	Ｘ`:only-child`	|	同層(~)裡只有一個，且為Ｘ	|	p:only-child	|

◎ 是該層的「所有子元素」，若該層第Ｎ個非指定的元素，將不會生效。(備註1)

---

## 特定子元素歷遍
| Syntax |Mean  | Selector |     
| :-------- | :-------- | :-------- | 
|	X`:first-of-type`	|	同層(~)裡的第一個Ｘ	|	p:first-of-type	|
|	X`:last-of-type`	|	同層(~)裡的最後一個Ｘ	|	p:last-of-type	|
|	X`:nth-last-of-type`	|	同層(~)裡的倒數第 N 個Ｘ	|	p:nth-last-of-type	|
|	X`:nth-of-type( n )`	|	同層(~)裡的第 N 個Ｘ	|p:nth-of-type(2)		|
|	X`:nth-of-type( 2n )`<br/>~~~~~~~~~(`even`)	|	同層(~)裡的每一偶數個Ｘ	|	p:nth-of-type(2n)<br/>p:nth-of-type(even)	|
|	X`:nth-of-type( 2n+1 )`<br/>~~~~~~~~~~(`odd`)	|	同層(~)裡的每一奇數個Ｘ	|	p:nth-of-type(2n+1)<br/>p:nth-of-type(odd)	|
|	X`:only-type`	|	同層(~)裡只有Ｘ時的所有 Ｘ	|p::only-type|

◎ 是該層的「第Ｎ個特定元素」(備註1)

---

## root / 反選偽類 not / empty 
| Syntax |Mean  | Selector |     
| :-------- | :-------- | :-------- | 
|	X`:empty`	|	沒有子元素的 X	|div:empty		|
|	`:not( selector )`	|	不符合特定 selector	|		|
|	`:root`	|	文檔根元素	|:root		|

◎ [關於 `:root`｜Amos](https://ithelp.ithome.com.tw/articles/10228111)  
◎ [關於 `:not`｜MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:not) - 不能:not(`:not` / `:before` / `:after`)

---

## 狀態
| Syntax |Mean  | Selector |     
| :-------- | :-------- | :-------- | 
|	X`:target`	|	當前的 target (#)	|		|
|	X`:enabled`	|	可作用中的 input	|		|
|	X`:disabled`	|	禁用中的 input	|		|
|	input`:checked`	|	被勾選的 input	|		|

---

補充:

#### `-child` & `of-type`  的差異  
- `-child` :
  若同層裡有 `<div>`、 `<p>` 混排，指定 p:first-child，但在該層的第一個元素是 div 而不是 p 時，會選不到！  
  因 "-child" 選擇器指定的第 Ｎ 個是指該層的「所有元素」，而不是所有的 `<p>`裡的第 N 個 `<p>`。  
  想要直覺的該層所有 `<p>` 裡的第 N 個 `<p>` 要把 "-child" 改成 "of-type"。  
  ([偽類 child 和 of-type｜oxxo](https://www.oxxostudio.tw/articles/201405/css-selector.html))

#### 偽元素冒號 `:before` ／ `::before`？  
  - 兩個冒號(`::before`)是CSS3的寫法，為區分偽類與偽元素：
      - 偽元素 (pseudo element )：雖不是真正的元素，但有著和元素相同的特性
      - 偽類 (pseudo classes)：特殊狀態（例如`:hover`）
  - 但目前瀏覽器兼容 CSS2 寫法，偽元素不用兩個冒號(`:before`)也是可以的。  
  (除了`::selection` 語法是固定兩個冒號)
    
--- 
參考資料
- [偽類 child 和 of-type｜oxxo](https://www.oxxostudio.tw/articles/201405/css-selector.html)
- [CSS Selector|MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [:root｜Amos](https://ithelp.ithome.com.tw/articles/10228111)  

---

⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10243699)



