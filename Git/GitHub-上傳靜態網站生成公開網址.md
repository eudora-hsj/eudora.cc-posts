---
title: '[GitHub] 使用GitHub上傳靜態網站作品生成公開網址　'
tags: [Git, GitHub]
category: Git
#   - - (所有文章)
#   - - 工程師－攻城路
#     - Git
#   - - 數位人－愛應用
#     - 軟體工具
permalink: posts/45315
date: 2020-04-19 00:45:19
---
<!-- # [GitHub] 使用GitHub上傳靜態網站作品生成公開網址 -->

### [前提] 
你需要先具備：
- 會使用Git、有GitHub帳號、能新建 Repository 並上傳檔案至 GitHub
- 限定靜態網站

<!--more--> 
> GitHub 個人帳號名=username
> Repository名稱=repo

## 兩種公開網址：

### 1-個人GitHub帳號.io/

> https://username.github.io/
- Step1.新建Repo名為 username.github.io (要跟GitHub帳號一致)

***（此時你可能會因為網址而想要[修改你的GitHub帳號](/posts/45315/#想修改-GitHub-帳號)）***

![](https://i.imgur.com/1alqUsK.png)


- Step2.上傳網站專案，網址就會自動讀取根目錄 index.html 囉!



---

### 2-個人GitHub帳號.io/repo
> https://username.github.io/repo

- Step1.新建 Repository、放進專案（注意Repo的命名，會帶入網址內）

- Step2.在Repository 的 Setting 區開啟 Source

![](https://i.imgur.com/wV9r34T.png)
![](https://i.imgur.com/cR9wUI1.png)


- Step3.複製網址即可連結成功囉！（首頁為根目錄的index.html）


## 延伸應用

### 想修改 GitHub 帳號

![](https://i.imgur.com/roOps0T.png)

注意！

修改 GitHub 帳戶的話原本的個人GitHub網址
也會變動，舊帳號網址GitHub並不會自動轉址！


---

### 想塞在同一個Repo

若想在同個 Repository 下放置多個不同暫時存放的靜態網頁專案時，可建子資料夾
(例如 projectA / projectB) 
> https://username.github.io/repo/projectA 
>https://username.github.io/repo/projectB



## 參考資料
- [使用 GitHub 免費製作個人網站 - 為你自己學 Git | 高見龍](https://gitbook.tw/chapters/github/using-github-pages.html)
- [GitHub Pages](https://pages.github.com/)