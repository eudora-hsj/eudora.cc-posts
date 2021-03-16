---
title: '[Git] 初始設定'
tags: [Git]
category: Git
#   - - (所有文章)
#   - - 工程師－攻城路
#     - Git
permalink: posts/31488
date: 2020-09-20 23:55:58
---

關於 Git 的初始設置與遠端 Repo 連結

<!--more--> 

---

## 一、前置作業

### 1.安裝 Git

~~google 一下發現教學文太多，加上實在不想重裝自己的 Git 還得 windows mac都來一遍……決定偷懶~~  
雙手奉上傳送門：

 - Mac OS： [為你自己學 Git](https://gitbook.tw/chapters/environment/install-git-in-mac.html)　｜  [六角學院](https://w3c.hexschool.com/git/fd6f6be)
 - Windows： [為你自己學 Git](https://gitbook.tw/chapters/environment/install-git-in-windows.html)　｜ [六角學院](https://w3c.hexschool.com/git/3f9497cd)


### 2.安裝 Git GUI (推薦 Sourcetree )

圖像化界面的 Git 操作工具，可以不使用 command line 進行 Git 的操作。但新手上路仍建議先以 command line 來進行學習，GUI 軟體只作為輔助使用（視覺化呈現目前的 Commit 歷程）  
眾多 Git GUI 軟體中推薦 Sourcetree：
- [Sourcetree](https://www.sourcetreeapp.com/)

### 3.選定 Git 程式碼託管服並綁定裝置與帳號

1. 註冊 GitHub (或其他常見的服務平台如 GitLab、Bitbucket）  
2. 設置 SSH key  

    實際應用時，在本地輸入指令 git push 就可以推上去指定的儲存庫，但 GitHub 怎麼判斷這個儲存庫誰可以上傳上來呢？我們可以設置 ssh key 讓 GitHub 去控管權限。

    在終端機中生成為一組成對的公鑰、私鑰，將公鑰設定在 GitHub 中，共 GitHub 透過比對公、私鑰是否對得起來而控制上傳權限。
    
- `$ ssh-keygen`  
    在終端機中產生金鑰
- `$ ls -al ~/.ssh `  
    查詢是否有 SSH Key了(出現檔案id_rsa.pub 或 id_dsa.pub 就成功囉)  
- `$ pbcopy < ~/.ssh/id_rsa.pub`  / `$ clip < ~/.ssh/id_rsa.pub`  
     複製公鑰 ( Mac / windows )

- 至 GitHub 的 [Setting 頁](https://github.com/settings/keys) 貼上 SSH Key就完成配置囉！


---

## 二、將專案導入 Git


> 好的，目前我假設你已經…
> 1. 安裝好 Git
> 2. 安裝好 Sourcetree 或其他 Git GUI
> 3. 已經註冊好 GitHub 或其他服務平台並且也設置好 SSH 了


### 1.以終端機開啟 目標資料夾(專案資料夾)
- Mac：`$ cd /c/project`
- Windows：`$ cd /mnt/c/project`
- VS Code 偷懶法： 先以 VS Code　開啟專案資料夾，再使用快鍵　Cmd + \` (Ctrl +  \`)　開啟終端機，預設所在路徑即為專案資料夾囉。


### 2.專案初始化 Git 並連結遠端儲存庫

-  `$ git init`   
    將專案資料夾初始化 Git
    ( Terminal 位置要在專案資料夾喔！ )
    
- 在 GitHub 中建立 Repository 並複製 SSH 位址
    - ![](https://i.imgur.com/IoiYOGY.png)
    
    - ![](https://i.imgur.com/VVPrimU.png)
<!--     - ![](https://i.imgur.com/zP3j5Cy.png) -->
    
- 回到終端機進行設置：
    - `$ git config --global user.name name`  
    - `$ git config --global user.email Email`  
    配置你的 username 與 email　(與 GitHub 帳號、Email 一致)


- `$ git remote add origin repositoryURL`  
連結遠端Repo (repositoryURL = 剛剛複製的那個 SSH 位址)

- `$ git remote -v`  
查詢是否綁定成功



---

## 三、推上遠端儲存庫

### 提交第一個 commit

完成設置後，就來進行第一次 commit 吧！  
可以先新增一個 readme.md 為這個專案進行簡單的介紹。  
完成後就進行未來會使用相當頻繁的 add、commit、push 三指令：

- `$ git add readme.md`  
    將 readme.md 檔加至暫存區

- `$ git commit -m'commitInfo'`  
    將暫存區檔案 commit 並寫上 commit 訊息

- `$ git push -u origin master`  
    推上 origin master (剛剛綁定的遠端Repo的分支Master  
  (使用 -u 指令等於指定了預設值，之後簡略只打 `git push`　就推至預設的 origin master)

完成大業！上去 GitHub 看有沒成功！

---

## 細節補充

### Ｑ："origin" 是固定語法嗎？

`$ git push 自訂的儲存庫名　對應的分支名`

origin 並不是固定的語法，有時我們同一個專案可能會綁定連結多個遠端儲存庫，push 到不同的遠端 Repo去，所以 push　後面接的是指定要推到「哪一個遠端儲存庫」裡的「哪一支分支」。

而這個自訂的儲存庫名在剛開始用 `$ git remote addo rigin repositoryURL` 指令時定義囉，（但並不會影響遠端儲存庫的名字，只是方便你識別你的多個遠端連結而已）。

---

## 同場加映－關於權限綁定

### Q：如何在多台電腦也能推上自己的 GitHub 帳號裡的 Repo？

- 方法1. 一樣做法，將第二台電腦的 SSH Key(公)登錄至 GitHub Setting 
- 方法2. 直接將第一台電腦的 SSH Key(私鑰) copy 給第二台電腦  
      （注意！此作法最好只用在自己的個人電腦，如果是公司電腦或他人電腦請勿這樣使用！）


### Q：如何在同一台電腦以不同的帳號身分推至對應的 GitHub?
（適用情境：公司電腦已有設置公司專用的 GitHub 帳號在 git config --global，但我想同時使用公司電腦應用自己私人 GitHub 帳號的專案，推上去時卻不會顯示自己的個人帳號）

![](https://i.imgur.com/P6k6B1B.png)

1. 同樣要先將公司電腦的 SSH Key 登錄至 GitHub Setting，此時公司電腦可以推你的個人帳號的 Repo，但並不會真正連結成自己的個人帳號。

2. 在 git config --local 設定自己個人帳號的 user name、email  
    - `git config --local user.name name`  
    - `git config --local user.email Email`	  

    `git config ---local `的設定只針對單一專案，也就是當你開啟了第二個個人專案時，也要先對該專案配置`git config --local `，否則預設都會吃 `git config --global`的設定。

總結：  
- SSH Key 設置成功 = 這個裝置被允許能進此 Repo。  
- 顯示的作者為何，由 git config 中設定，而預設為 global 的設定，有指定 local 的設定時才會被覆蓋。

---


參考資料：


- [Git 教學 - Git 書 - 為你自己學 Git | 高見龍](https://gitbook.tw/)
- [ASTRO X 五倍紅寶石 全端工程師實戰訓練營 | 高見龍](https://astro.5xruby.tw/)
- [六角學院](https://w3c.hexschool.com/git/3f9497cd)


---


⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10240965)
