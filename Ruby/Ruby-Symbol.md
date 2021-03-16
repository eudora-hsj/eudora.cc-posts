---
title: '[Ruby] 圖說 Ruby 世界中的 Symbol (符號)'
permalink: posts/43666
date: 2020-04-15 23:06:28
tags: [Ruby, Symbol]
category: Ruby
#   - - (所有文章)
#   - - 工程師－攻城路
#     - Ruby/Rails
---

# Ruby 中的 Symbol （符號）
一個有「名字」的「物件」  
<!--more--> 
一個有「名字」的「物件」  
一個有「名字」的「物件」  

# Symbol （符號）
顯示出特別意義，以供辨識的記號。（辭典）

我的白話文：本身代表著某個意義的東東 就像看到「3」就知道代表著 OOO ← 三個

## 是一個已存在的物件
- 符號是一個物件（存於記憶體中的一格）  
對比：變數（Variable） 必須被賦予值才能存在

## 語法固定以「：」開頭
:XXX 開頭冒號的是 Symbol  
:XXX 開頭冒號的是 Symbol  
:XXX 開頭冒號的是 Symbol  
![](https://i.imgur.com/28Gf1C6.png)
* 名字語意是業障，只管看它開頭有「：」就是 Symbol 啦！
![](https://i.imgur.com/GS46TyK.png)
## Symbol 在記憶體空間位址不變
* Symbol 是個喜歡定點長住的愛家人士、不是漂泊型的旅客：
![](https://i.imgur.com/EVRDGTp.png)
* 對比：字串（String）的差異：
![](https://i.imgur.com/bzh99tc.png)
每次出場都重開新房間
![](https://i.imgur.com/hrqf4EO.png)
String 每次出場都有新的 object_id ！（參考上圖紅色星號）
* 在記憶體未清空時呈現這樣的狀況：
![](https://i.imgur.com/D1XVnGM.png)
你以為 String一直得到新房間是比符號尊貴嗎？ 不……當管理大樓想開始清掃房客時，符號才是不會被趕走的真住客！
![](https://i.imgur.com/lHinHBp.png)
** 備註：Ruby 後期版本有其他方法能夠指定清空記憶體時連同符號一起清除 **

## 總結+補充 幾點特性
* Symbol 本身就是一個物件，可以單獨存在著、也可以當「值」指給 Variable （不像 Variable →沒有存值就不存在）

* 難道沒有人想依附的人就不配活著嗎？單身狗ＱＱ

* Symbol 不可變！String 卻可以被改變

* 就像我是 Eudora 、不要嫌三個音麻煩想叫 Dora 啊！畫風瞬間變幼幼卡通台

* 一個 Symbol 只會有一個固定不變的object_id，故多次存取時效能較 String 佳  
（String 每次重新占用一個object_id）  
相反面：佔住的這一格也就沒這麼輕易能清空、釋放出空間
  因上述特性而常被應用在當 Hash 的 key  


---

嗯～可獨立生活／專一不變／住家位置固定好找／不開分身術不會亂亂跑
Symbol 似乎是個挺穩重可靠、可託付終身的傢伙呢！（誤XD）


---

參考資料
[書籍：為你自己學 Ruby on Rails | 高見龍](https://railsbook.tw/)
[課程：ASTRO Camp](https://astro.5xruby.tw/)

