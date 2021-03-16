---
title: '[Git] 在 VS Code 中的基本應用'
tags: [Git, VSCode]
category: Git
#   - - (所有文章)
#   - - 工程師－攻城路
#     - Git
#   - - 工程師－攻城路
#     - Editor
permalink: posts/31490
date: 2020-09-22 21:15:26
---


簡介在 VS Code 中查看檔案狀態

<!--more--> 

---

[上一篇](https://eudora.cc/posts/31487/)提到的 Git 傳送階段：
![](https://i.imgur.com/7rrUAmO.png) 

---

如果你使用 VS Code 開啟有導入 Git 並連結遠端 Repo 的專案時，左側會有 Git 面板可清楚查看你的檔案編輯狀態：

---

### 【Changes】－紀錄有變動的檔案（相當於第一階段 Working Directory） 
 
![](https://i.imgur.com/BkpaExi.png)

- 點 (1) 檔案名稱-檢視該檔且比對變動處
    ![](https://i.imgur.com/z1WwViI.png)  
    超實用！每次完成一個功能時我會透過這個方式來逐一確認變動處。
- 點 `(2) Open File` 開啟該檔案 
- 點 `(3) Discard Changes` 取消變更（直接將檔案恢復到更動前）  
    不小心把某個檔案改爛了想砍掉重來嗎？不用再靠記憶力或提前複本啦！一鍵按下去直接恢復原版啦！
- 點 `(4) Stage Changes` 加入至暫存區：相當於執行 `git add (file)` 等於將檔案交到暫存區囉！

### 【Staged Changes】－暫存區檔案（= git add 進來的檔案）

![](https://i.imgur.com/sAqtJLo.png)

透過`git add` 或前述的一鍵大法，就會發現有檔案跑進 Staged Changes 區了。  
- 在這裡點擊檔名一樣是檢視檔案比對變動處（但卻會呈現被鎖住的、無法編輯的狀態）：
    ![](https://i.imgur.com/npM7ZU9.png)

- 想再退回前一個階段（移除暫存區），使用－按鈕相當於下指令 `git reset (file)`。

    ![](https://i.imgur.com/bFbcR2h.png)

---

好的，討厭 command-line 的同學們，靠 VS Code　這左側欄就可以不用 git add / git reset 了，但是原理還是要理解哦！話說用指令操作其實也有它方便的地方，例如變動了Ｎ個檔案時，使用`git status` 查看（如圖）：

![](https://i.imgur.com/1ub52wE.png)  
我只想 add 所有 js 資料夾底下的，這時使用指令下 `git add js/`  
![](https://i.imgur.com/zaO73P1.png)  
就可以很快速地只對特定資料夾進行 git add 囉！


---

## commit！

前面會了 git add / git reset 來將檔案存放至暫存區。暫存區的概念可以想像成你包裝好的貨物陸續堆放在待出貨區，可以陸續地將改好的檔案堆在這，下個階段就是 git commit 提交成一個版本囉！  

為什麼分兩階段？
試想你可能同時改多個功能、動到許多檔案，但某些功能要先提交，或者是已經確定沒問題不會再動了，這時有暫存區可以清楚區分這些已「預計可提交」的檔案，相當方便管理！

執行　`git commit` 作用檔案範圍是「暫存區的所有檔案」，有變動但未加到暫存區（也就是剛剛再 VS Code 的 [Changes] 內）的檔案是不會被 commit 的哦

![](https://i.imgur.com/WVJ9lU9.png)


當你 commit 之後會發現這裡就清空了，可知這裡所做的「更動比較」是跟「目前的 commit」 比較。

![](https://i.imgur.com/aPGrxeI.png)

到此時都還只是在本地端的操作，直到執行 `git push` 才真正推送到遠端讓他人看得見。
（也就是在 push 之前發現 code 有問題都還可以在被看見之前手刀修改 XD~）

---

回想起自己剛用 VS Code、剛學 Git 還是沒發現這區面板的神奇妙用，當時用 command-line 操作 status / add / commit 也還不熟（所以到底在下什麼指令XD？），後來指令漸漸熟了，忽然也看懂這區面板了！新手上路先搞清楚傳送階段後，使用 command-line + VS Code 這區 source control + soucetree　+ 實際練習，就能手刀上手了！

<!-- 接下來直接舉例幾個常見的應用情境（不用 VS Code / soucetree 一鍵大法）：

---

## 如何取消 git add?

Q: 下了 git add (檔案)後，後悔了怎辦？  
A: `git reset (檔案)`

---

## 如何取消 commit ?

Q: 剛 commit 完後悔了!  
A: `git reset HEAD^`

---

## git push 時發現落後遠端目標分支

Q: 不想執行 merge、不想長出支線，想從遠端分支最新 commit 往前長
A: git pull --rebase
> 也可以 pull rebase 不同分支喔，例如處在自己的 feature 分支，想 pull master： `git pull --rebase origin master`，可以邊在自己的分支開發時又持續抓取 master 最新版。

---

## 我想建立新分支並直接切過去

Q: `git branch (newBranchName)` 再 `git checkout (newBranchName)` 好麻煩！
A: `git checkout -b (newBranchName)
 -->

---


參考資料：
- [Git 教學 - Git 書 - 為你自己學 Git | 高見龍](https://gitbook.tw/)
- [ASTRO X 五倍紅寶石 全端工程師實戰訓練營 | 高見龍](
https://astro.5xruby.tw/)

---


⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10242283)
