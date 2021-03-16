---
title: '[Git] 基礎觀念'
tags: [Git]
category: Git
#   - - (所有文章)
#   - - 工程師－攻城路
#     - Git
permalink: posts/31487
date: 2020-09-19 23:45:17
---

簡介 Git、GitHub、版本控制
<!--more--> 

---

## Git 是什麼？
- Git 是眾多版本控制工具中的其中一個工具（版本控制工具不等於 Git ）
    - 是目前業界最多人使用的版控軟體


- 免費、開源、體積小速度快
- Git只能建立不能破壞
    - 沒有「剪下」貼上，只有「複製」貼上
    - Git 不會刪除 Commit，最多只是「隱藏」（看不見）
- Git 是透過快照紀錄(類似照片存檔)的概念、而非每一個版本全檔備份
    - 適合版控文字型態文字檔(程式)：文字差異比對
- 共有100多個指令（但其中10～20幾個指令就夠日常應用）

## Git？GitHub？傻傻分不清楚？

前文提到，Git 是一種版控工具，而 GitHub、GitLab 是一個商業網站（本體是一個 Git 伺服器），以 Web 介面操作Git，故 Git 不等於 Git Hub 喲！

---

## [必知基本觀念] 傳送四階段
- ![](https://i.imgur.com/nYxcP8B.png)

不過就操作與意象上，由下往上似乎更直覺：
![](https://i.imgur.com/7rrUAmO.png) 

### 1.工作目錄－Working Drectory 
這一個階段只是記錄檔案變動狀態。(類似貼標籤記錄)

### 2.暫存區域 　－Staging Area
有變動的檔案在使用 git add 指令時才會進入此區

### 3.儲存庫(本地)　－Local Repository
使用 git commit 指令將暫存區的檔案 commit，紀錄於 Local Repo

### 4.儲存庫(遠端)　－Remote Repository
直到使用 git push 指令才推上遠端儲存庫（如 Git Hub / GitLab）

---
## [Commit] 

commit 是以快照的方式記錄目錄文件的變化，而非每次都複製所有檔案，故可以快速切換讓專案回到各個 commit 階段，有如坐時光機一樣，秒切換到各個版本之間做彈性的應用。


## [Branch 分支]

- 分支可應用在於多人開發 / 新功能開發（區分 正式發佈 / 開發階段 ...等），在不影響主線的狀況下開發，直到功能到一個段落之後再合併至主線。

- 主線通常會被加以保護，自分支完成階段開發後，提出合併回主線的申請 PR－Pull Request（ GitHub 中的 PR 等同於Git Lab中的 MR - Merge Request）

- 建立分支的動作其實只是「在目前的 commit 貼上一張有名字的貼紙」，再進行下一次的 commit 之前，其實並沒有任何變化。


## [HEAD]

- HEAD 類似磁頭的概念，表示目前指向哪一個分支 Branch
- 而分支 Branch 其實只是貼在 Commit 上的貼紙


![](https://i.imgur.com/bbttzpQ.png)


---


## [補充] 關於版本控制

### 版本控制系統 Version Control System
- 更有效率的備份系統
- 歷史紀錄及證據(出事時就可以知道從何時開始有問題)
- 分集中式／分散式
    1. 集中式的版控系統 Centralize Version Control
        - 依靠中間的Server
        沒有網路或沒有Server時就沒有辦法運作版控
        - 如 CVS 或 SVN
    3. 分散式的版控系統 Distributed Version Control
        - 可以不透過中間 Server 直接傳給另一個人
        - 如 Git（目前主流）

---


在學 Git 各種進階指令前，最最最基本功 Git clone / init / add / commit / pull / push / merge / rebase 及 branch 的切換先練習至上手，再去應用進階的後續指令吧！

回想自己剛學 Git時一陣茫，好像有聽懂、卻又感覺有點抽象，直到真正進行多人協作時才真的懂了 Git 在做什麼，也才發現在開發上是多麼重要的應用！即使不是多人協作，使用 Git 管理自己的專案也是相當必要的。

還沒有實際使用過 Git 的人，只看上述的觀念篇大概會覺得有些抽象，等實作中踩過幾次雷就會越來越能夠掌握囉！

---

參考資料：
- [Git 教學 - Git 書 - 為你自己學 Git | 高見龍](https://gitbook.tw/)
- [ASTRO X 五倍紅寶石 全端工程師實戰訓練營 | 高見龍](
https://astro.5xruby.tw/)

---


⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10240279)
