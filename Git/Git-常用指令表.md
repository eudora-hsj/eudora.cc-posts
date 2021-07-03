---
title: '[Git] 常用指令表'
tags: [Git, CLI]
category: Git
permalink: posts/31489
date: 2020-09-21 21:14:46
---
這篇整理常用的 Git 指令表。

<!--more--> 
---

## SSH Key

- `$ ssh-keygen`  
    在終端機中產生金鑰
- `$ ls -al ~/.ssh `  
    查詢是否有 SSH Key了(出現檔案id_rsa.pub 或 id_dsa.pub 就成功囉)  
- `$ pbcopy < ~/.ssh/id_rsa.pub`  / `$ clip < ~/.ssh/id_rsa.pub`  
     複製公鑰 ( Mac / Windows git bash )
 
 
 
## config

 | Git                                          | zsh  | do         | Remark |
 | :------------------------------------------- | :--- | :--------- | :----- |
 | `git config --list`                          | gcf  | 查看設定   |        |
 | `git config --local user.name "(userName)"`  |      | 設定帳號   |        |
 | `git config --local user.email "(e-mail)"`   |      | 設定E-mail | 全域   |
 | `git config --global user.name "(userName)"` |      | 設定帳號   | 單專案 |
 | `git config --global user.email "(e-mail)"`  |      | 設定E-mail | 單專案 |


### init / clone
 | Git           | zsh  | do               | Remark |
 | :------------ | :--- | :--------------- | :----- |
 | `git clone`   |      | 抓遠端儲存庫下來 |        |
 | `git init `   |      | Git 初始化       |        |
 | `rm -rf .git` |      | 移除 Git         |


## remote
 | Git                                       | zsh  | do                | Remark |
 | :---------------------------------------- | :--- | :---------------- | :----- |
 | `git remote add (origin) (git@~.git)`     | gra  | 遠端連結          |        |
 | `git remote set-url (origin) (git@~.git)` |      | 修改遠端連結      |        |
 | `git remote remove (origin)`              | grrm | 移除遠端連結      |        |
 | `git remote -v`                           | grv  | 查詢遠端連結(URL) |        |
 | `git push -u (origin) (master)`           |      | 推上遠端並綁定    |        |


## 基本版更（ pull / push / add / commit / status /fetch）

 | Git                                   | zsh         | do                        | Remark       |
 | :------------------------------------ | :---------- | :------------------------ | :----------- |
 | `git status`                          | gst         |                           |              |
 | `git add (file)`                      | ga (~)      |                           |              |
 | `git add .`                           | ga .        |                           |              |
 | `git commit -m'message'`              | gcmsg '(~)' |                           |              |
 | `git commit --amend`<br>              |
 | `git commit --amend -m'message'`      |             | 修改最後一次的commit      |              |
 | `git pull`                            | gl          |                           |              |
 | `git push (remote) (branch)`          | gp (~) (~)  |                           |              |
 | `git push -u  (remote) (branch)`      | gp -u       |                           |              |
 | `git restore --staged (file)`         |             | 取消 git add              |              |
 | `git pull --rebase (remote) (branch)` | gup          |                           |              |
 | `git fetch`                           | gl          | 獲取remote                |              |
 
 
 
 <!-- | XXX 至當前當前分支                    | `gg`pull    | git pull (current_branch) | push... 等同 | -->
 
 
 
## 檔案變更版更操作
 | Git                   | zsh  | do                     | Remark                          |
 | :-------------------- | :--- | :--------------------- | :------------------------------ |
 | `git clean -fd`       |      | 清除未被追蹤的所有檔案 | 已編輯的會恢復,新增的不會變動   |
 | `git checkout (file)` | gco  | 當前目錄回復前次存檔   | (已編輯的會恢復,新增的不會變動) |
 | `git restore (file)`  | grs  | 當前目錄回復前次存檔   | (含被刪除的檔)                  |
 
 

## Branch 分支

 | Git                                 | zsh  | do                     | Remark             |
 | :---------------------------------- | :--- | :--------------------- | :----------------- |
 | `git branch`                        | gb   | 查詢所有本地分支       |                    |
 | `git branch -a`                     | gba  | 查詢所有遠端分支       |                    |
 | `git branch (newBranch)`            |      | 當前 commit 新建分支   |                    |
 | `git branch (newBranch) (commitID)` |      | 特定 commit 上新建分支 |                    |
 | `git checkout (branch)`             | gco  | 切換到某分支           |                    |
 | `git checkout -b  (newBranch)`      | gcb  | 新建分支並切換過去     |                    |
 | `git branch -d (branch)`            |   | 刪除某分支             |                    |
 | `git branch -D (branch)`            |      | 強制刪除某分支         |                    |
 | `git branch -m  (branch) (newName)` |      | 將某 branch 更名       | 必須先切到不同分支 |
 

---

## Reset 還原

| Git                          | zsh | do                                    | Remark             |
| :--------------------------- | --- | :------------------------------------ | :----------------- |
| ` git reset (commit) `       |     | 還原工作目錄與索引                    | 預設為'mixed'      |
| `git reset (commit) --mixed` |     |                                       | 放回"1-工作目錄"   |
| `git reset (commit) --soft ` |     |                                       | 放回"2-暫存區"     |
| `git reset (commit) --hard`  |     |                                       | 都不留(直接被隱藏) |
| `git reset (commit)^`        |     | 退回前1次的commit                     | ^^ 退回前2版…      |
| `git reset (commit)~5`       |     | 退回前5次的commit                     | ~N 退至前N版       |
| `git reset --hard HEAD@{1}`  |     | 取消剛剛的Reset | 快進下一個commit   |


* (commit)可以是 branch / commit ID / HEAD^

- `git reset --soft HEAD^ `：拆掉最近一次commit但保留異動內容 
- `git reset --hard HEAD^ `：拆掉最近一次 commit 
- `git reset --hard ORIG_HEAD`：取消剛剛拆掉的 commit
 

---
## Rebase  合併應用

| Git                   | zsh | do             | Remark |
| :-------------------- | --- | :------------- | :----- |
| `git rebase (branch)` | grb | 重接分支基底   |        |
| `git rebase --continue` |  | 繼續 rebase   |        |
| `git rebase --abort` |  | 取消 rebase   |        |

## Merge 合併應用
| Git                   | zsh | do             | Remark |
| :-------------------- | --- | :------------- | :----- |
| `git merge (branch)`  | gm  | 合併分支(平行) |        |
| `git merge --abort`<br> `git reset --merge`  |   |取消 merge |        |

<!-- - rebase : rebase 每次 commit 多重確認，分支 X 
- merge : 2 支分支最新版合併，分支X merge Y 等於 將 Y 合併到 X ( X 為主角)  -->

---

## 查詢
| Git                               | zsh | do                     | Remark        |
| :-------------------------------- | --- | :--------------------- | :------------ |
| `git config --list`               | gcf | 查詢目前設定           |               |
| `which git `                      |     | 查詢 Git 位置          |               |
| `git --version`                   |     | 查詢Git版本            |               |
| `git status`                      | gst | 查詢狀態               |               |
| `git log`                         |     | 查詢 Log               |               |
| `git log --oneline`               |     | 查詢 Log(單行顯示)     |               |
| `git log --oneline --all --graph` |     | 樹狀圖形檢視 Log           |               |
| `git log -p FileName`             |     | 查詢檔案 Log           |               |
| `git blame FileName`              |     | 查詢該檔案每行編輯資訊 | (上傳者&時間) |
| `git reflog`                      |     | 查詢 reflog            |               |
| `git help`                        |ghh| 查詢指令               |               |



-  reflog：reflog保留HEAD移動的軌跡，可以查詢到commit ID(用於尋找被隱藏的commit)


## Tag 標籤 
| Git                                 | zsh | do           | Remark |
| :---------------------------------- | --- | :----------- | :----- |
| `git tag`                           |     | 查詢標籤     |        |
| `git tag -n`                        |     | 查詢詳細標籤 |        |
| `git tag (標籤名)`                  |     | 新增輕量標籤 |        |
| `git tag -am "(備註文字)" (標籤名)` |     | 新增標示標籤 |        |
| `git tag -d (標籤名)`               |     | 刪除標籤     |        |
| `git push origin --tags `               |     | 將標籤推至遠端     |        |

- （於目標分支且拉最新 `git checkout master`、`git pull`）
- 本地打 tag : `git tag 20200913`
- 推至遠端：`git push origin --tags`

## stash  暫存 
| Git               | zsh | do               | Remark |
| :---------------- | --- | :--------------- | :----- |
| `git stash`       |gsta| 暫時儲存當前目錄 |        |
| `git stash save -u <名稱>` |     | 暫時儲存且命名     |        |
| `git stash list` |gstl| 瀏覽 stash 列表  |        |
| `git stash apply`<br>`git stash apply stash@{0}` |gstaa| 還原最新但不刪除<br>還原~但不刪除     |        |
| `git stash pop`<br>`git stash pop stash@{0}`   | gstp | 還原最新暫存<br>還原~且刪除         |        |
| `git stash drop` <br>`git stash drop stash@{0}` |gstd| 清除最新暫存<br>清除~暫存      |        |
| `git stash clear` |gstc| 清除全部暫存     |        |



## 其他
| Git               | zsh | do               | Remark |
| :---------------- | --- | :--------------- | :----- |
| `git diff <commit1> <commit2> `     |  |  查看兩個commit的差異  | |        
| `git cherry-pick commit`        |    | |        |
| `rebase -i commit`        |   | |        |
| `git clean -fd`        |   |將目前Untracked的檔案全部刪除 |        |
| `git cherry-pick -h`        |   |查詢cherry-pick相關指令 |        |



---
參考資料：
- [Git 教學 - Git 書 - 為你自己學 Git | 高見龍](https://gitbook.tw/)
- [ASTRO X 五倍紅寶石 全端工程師實戰訓練營 | 高見龍](
https://astro.5xruby.tw/)

---

⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10241407)

