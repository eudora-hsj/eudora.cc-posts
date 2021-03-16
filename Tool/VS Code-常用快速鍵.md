---
title: '[Editor] VS Code 常用快速鍵'
tags: [Editor, VSCodde]
category: Editor/IDE
#   - - (所有文章)
#   - - 工程師－攻城路
#     - Editor
permalink: posts/31485
date: 2020-09-17 08:32:31
---

列表常用的 VSCode 快速鍵。

<!--more--> 

---

## Visual Studio Code
  
工欲善其事必先利其器，好的 Editor / IDE 讓你開發速度加倍速，爛的編輯器讓你倒退嚕。  
再把快速鍵的手感練起來，整個寫 Code 速度就是快的不要不要的，沒有滑鼠也能飛起來！（~~是要飛去哪啦！？~~）


![](https://i.imgur.com/VFRPsqv.png)

選擇 VS Code 主要原因:

1. 輕量
2. 插件多
3. 使用戶多  
~~4. 轉職前看到前端工程師同事在用~~  
~~5. 轉職進修中看到講師們在用~~  
~~6. 轉職後看到公司同事在用~~  


嘿啦～反正就這樣。直接送上[ VS Code 下載傳送門](https://code.visualstudio.com/download)

相信你載了之後摸個幾下就會使用了吧～我假設你秒會開啟檔案/開啟資料夾新增／編輯檔案囉！（超不負責任的教學文XD）。那就接著分享我個人常用的快速鍵：

---


### 開啟/關閉 檔案&專案資料夾

| Hotkey             | Mac                          | Windows                          | Remark |
| :----------------- | :--------------------------- | :------------------------------- | ------ |
| 開啟文件           | `Cmd` + `O`                  | `Ctrl` + `O`                     | -      |
| 開啟資料夾         | `Cmd` + `K` + `L`            | `Ctrl` + `K` + `L`               | -      |
| 儲存文件           | `Cmd` + `S`                  | `Ctrl` + `S`                     | -      |
| 儲存所有文件       | `Cmd` + `Option` + `S`       | `Ctrl + k` 　 `S`                | -      |
| 另存新檔           | `Cmd` + `Shift` + `S`        | `Ctrl` +`Shift` +  `S`           | -      |
| 開新檔案           | `Cmd` + `Ｎ`                 | `Ctrl` + `Ｎ`                    | -      |
| 開新VSCode視窗     | `Cmd` + `Shift` + `Ｎ`       | `Ctrl` + `Shift` + `Ｎ`          | -      |
| 關閉檔案/關閉窗格  | `Cmd` + `W`                  | `Ctrl` + `W`  <br> `Ctrl` + `F4`   | -      |
| 關閉所有檔案       | `Cmd + ｋ` `Cmd` + `W`       | `Ctrl + k` 　`Ctrl + W`          | -      |
| 關閉整個 VS Code   | `Cmd` + `Shift` + `W`        | `Ctrl` + `Shift` + `W`           | -      |
| 快速搜尋檔案並開啟 | `Cmd` + `P`                  | `Ctrl` + `P`                     | 註1    |
| 命令列             | `F1` <br>`Cmd` + `Shift` + `P` | `F1` <br> `Ctrl`  + `Shift` +  `P` | 註1    |


備註  
1.  開頭輸入 `>` 為指令模式；沒有 `>` 開頭時為搜尋檔名快速開啟。

---

### 面板開關/設定/編輯檢視設定

| Hotkey                            | Mac                                           | Windows                   | Remark |
| :-------------------------------- | :-------------------------------------------- | :------------------------ | :----- |
| [VS Code] 放大                    | `Cmd` + `+`                                   | `Ctrl` + `+`              | -      |
| [VS Code]  縮小                   | `Cmd` + `Shift` + `+`                         | `Ctrl` + `-`              | -      |
| [Scroll Page ] 往上滾 / 往下滾    | `Cmd` + `↑` / `↓`                             | `Ctrl` + `↑` / `↓`        | -      |
| [面板開/關] 側欄                  | `Cmd` + `B`                                   | `Ctrl` + `B`              | -      |
| [面板開/關] 插件                  | `Cmd` + `Shift` + `x`                         | `Ctrl` + `Shift` + `X`    | -      |
| [面板開/關] 終端機                | `Cmd` +  \`                  | `Ctrl` +    \` | -                         |
| [面板控制] 新開終端機             | `Cmd` + `Shift` + ` \`                        | `Ctrl` + `Shift` +   \`   | -      |
| [面板控制] 分割視窗方式新開終端機 | `Cmd` + `\`                                   | `Ctrl` + `Shift` +  `5`   | -      |
| [面板開/關] 下方面版              | `Cmd` + `J`                                   | `Ctrl` + `J`              | -      |
| [切換開啟中的檔案] 當前窗格的     | `Cmd` + `Shift` + `[` / `] `                  | `Alt` + `→`  / `← `       | -      |
| [切換開啟中的檔案] 列表往下選<br>~~~~~~~~~~~~~~~~~~往上選     | `Ctrl` + `tab` <br> `Ctrl`  + `Shift` + `tab`   | `Ctrl` + `tab` <br>  `Ctrl`  + `Shift` + `tab`   | -      |
| [切換檔案] 所在窗格的檔案         | `Control` + `1` / `2` ...                     | `Alt` + `1` / `2` ...     |        |
| [切換檔案] 切換/新增第Ｎ個窗格    | `Cmd` + `1` / `2` ...                         | `Ctrl` + `1` / `2` ...    | 註1    |
| [文檔檢視] 自動折行檢視           | `option` + `Z`                                | `Alt` + `Z`               | 註2    |
| 用戶設置                          | `Cmd` + `,`                                   | `Ctrl` + `,`              |        |
| 快速鍵設置                        | `Cmd + K` `Cmd + S`                           | ` Ctrl + K` `Ctrl + S`    |        |


備註  
1. 沒有第Ｎ個分割窗格時等同於新開分割窗格
2. 只是方便檢視,非編輯文檔本身

---

### 編輯 Code 快鍵 - 當前行/跳至行 ...


| Hotkey                    | Mac                               | Windows                     | Remark     |
| :------------------------ | :-------------------------------- | :-------------------------- | :--------- |
| 復原                      | `Cmd` + `Z`                       | `Ctrl` + `Z`                | -          |
| 重做                      | `Cmd` + `Shift` + `Z`             | `Ctrl` + `Shift` + `Z`      | -          |
| 剪下                      | `Cmd` + `X`                       | `Ctrl` + `X`                | 註1        |
| 複製                      | `Cmd` + `C`                       | `Ctrl` + `C`                | 註1        |
| 貼上                      | `Cmd` + `V`                       | `Ctrl` + `V`                | -          |
| [刪除] 該行               | `Cmd` + `Shift` + `K`             | `Ctrl`  + `Shift` + `K`     | 多行也適用 |
| [刪除] 該行游標之後的文字 | `Ctrl` + `K`                      |                             | -          |
| [移動] 往上／下行移       | `Option` + `↑` / `↓`              | `Alt` + `↑` / `↓`           | 多行也適用 |
| [複製] 往上／下複製       | `Option` + `Shift` + `↑` / `↓`    | `Alt` + `Shift` + `↑` / `↓` | 多行也適用 |
| [縮排] 往後               | `Cmd` + `]` <br> `tab`              | `tab]`                      |            |
| [縮排] 往前               | `Cmd` + `[`  <br>  `Shift` + `tab]` | `Shift` + `tab]`            |            |
| 註解                      | `Cmd` + `/`                       | `Ctrl` + `/`                |            |
| 文件自動排版              | `Alt` + `Shift` + `F`             | `Alt` + `Shift` + `F`       | 註2        |


備註
1. 沒有選取字時也有效作用於整行
2. coding style 略有不同，使用自動排版務必謹慎。

---


### 游標快速跳至...
| Hotkey                   | Mac                        | Windows                 | Remark         |
| :----------------------- | :------------------------- | :---------------------- | :------------- |
| [跳至] 畫面上的首行/末行 | `Fn` + `↑` / `↓`           |                         | -              |
| [跳至] 文件第 1 行<br>~~~~~~~~最後 1 行        | `Cmd` + `↑` <br>   `Cmd` +  `↓`              | `Ctrl` + `Home`   <br>    `Ctrl` +  `End`     | -              |
| [跳至] 目前行 最前面<br>~~~~~~~~~~最後面     | `Cmd` + `←`  <br> `Cmd` +  `→`              |                         | -              |
| [選取] 至目前行 最前面<br> ~~~~~~~~~~~~最後面    | `Cmd`  + `Shift` + `←` <br>`Cmd`  + `Shift` +  `→`      |                         | -              |
| [選取] 向下選取相同字    | `Cmd` + `D`                | `Ctrl` + `D`            | 選取字時按.註2 |
| [選取] 選取所有相同字    | `Cmd` + `Shift` + `L`      | `Ctrl` +`Shift` + `L`   | 選取字時按     |
| [跳至] 前 / 後一個字     | `Option` + `←` / `→`       |                         | -              |
| [跳至] 更動處下一個<br> ~~~~~~~~~上一個      | `Option` + `F5`<br> `Option`  + `Shift` + `F5`            | `Alt` + `F5` <br>  `Alt`  + `Shift` + `F5`         | -              |
| [跳至] 該定義            | `F12`                      | `F12`                   | 註1            |

備註
1. 例如游標停留在變數或function name時，按F12將直接跳至其定義的行。
2. 沒選取字時將自動選取游標所在的單字


---


### 搜尋／取代
| Hotkey            | Mac                       | Windows                   | Remark               |
| :---------------- | :------------------------ | ------------------------- | :------------------- |
| [搜尋] 全專案     | `Cmd` + `Shift` + `F`     | `Ctrl` + `Shift` + `F`    | 左側搜尋/取代面板    |
| [搜尋] 特定資料夾 | `Shift` + `Option` + `F`  | `Shift` + `Alt` + `F`     | 左側選取資料夾後按   |
| [搜尋] 當前文檔   | `Cmd` + `F`               | `Ctrl` + `F`              | 可先選字再按鍵       |
| └ 選至下一個      | `Enter` <br> `F3`         | `Enter` <br> `Shift` + `F3` | -                    |
| └ 選至上一個      | `Shift` + `Enter`         | `Shift` + `Enter`         | -                    |
| └ 全選            | `Option` + `Enter`        | `Alt` + `Enter`           | -                    |
| [取代] 目前文檔   | `Cmd` +`Option` +  `F`    | `Ctrl` +  `H`             | 可先選字再按鍵       |
| └逐一取代         | `Enter`                   | `Enter`                   | 目前文檔取代結果時按 |
| [取代] 全專案     | `Cmd` + `Shift` + `H`     | `Ctrl` + `Shift` + `H`    | 左側搜尋/取代        |
| └ 進階篩選欄      | `Cmd` + `Shift` + `J`     | `Ctrl` + `Shift` + `J`    | 在搜尋/取代面板時按  |
| └全部取代         | `Cmd` +`Option` + `Enter` | `Ctrl` + `Alt` + `Enter`  | 列表取代結果時按     |

---

### 左側檔案列表區,點選特定檔案後...
| Hotkey                         | Mac                              | Windows                         | Remark |
| :----------------------------- | :------------------------------- | ------------------------------- | :----- |
| 以OS檔案總管開啟該檔所屬資料夾 | `Cmd` +`Option` +  `R`           | `Shift` + `Alt` + `R`           | -      |
| 複製該檔相對路徑               | `Cmd` +`Option` + `C`            | `Ctrl + k` 　`Ctrl + Shift + C` | 備註1  |
| 複製該檔絕對路徑               | `Cmd` +`Option` + `Shift` +  `C` | `Shift` + `Alt`+  `C`           | 備註1  |

備註：  
1. Path / Relative Path
    - 絕對路徑：...(略)/project/index.html 
    - 相對路徑：index.html   



---


### Formate 排版自動校正
| Hotkey         | Mac                      | Windows               | Remark                   |
| :------------- | :----------------------- | --------------------- | :----------------------- |
| 自動格式化排版 | `Option` + `Shift` + `F` | `Alt` + `Shift` + `B` | 需裝對應語言的 Formatter |

---


### 瀏覽
| Hotkey                 | Mac                      | Windows               | Remark |
| :--------------------- | :----------------------- | --------------------- | :----- |
| 預設瀏覽器開啟目前檔案 | `Option` + `B`           | `Alt` + `B`           | -      |
| 選擇瀏覽器開啟目前檔案 | `Option` + `Shift` + `B` | `Alt` + `Shift` + `B` | -      |


---


### 插件限定
| Hotkey             | Mac                     | Windows               | Extention                                                                                |
| :----------------- | :---------------------- | --------------------- | :--------------------------------------------------------------------------------------- |
| 將當前行加入至書籤 | `Cmd` + `Option` +  `K` | `Ctrl` + `Alt` + `k`  | [Bookmarks](https://marketplace.visualstudio.com/items?itemName=alefragnani.Bookmarks)   |
| 運行 Live Server   | `Cmd` + `L` + `O`       | `Alt` + `Shift` + `B` | [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) |

（↑ 這區快速鍵是特定插件定義的。）


---

### 完整快速鍵一覽表：
完整版：

- VS Code 官方快速鍵：[Windows](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)｜[MacOS](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
- 在 VS Code 按` Cmd + K  Cmd + S` （`Ctrl + K  Ctrl + S` ）開啟快速鍵一覽表或變更定義：

    ![](https://i.imgur.com/HzHnpOq.png)

---

上述為我平時寫 Code 會滿頻繁使用到的動作，相信看完上面的表格有些還是看不太出來怎麼用，自已在 VS Code 上 Try Try 吧！  

手感是時間累積讓肌肉去記憶，一剛開始操作特定動作時刻意地去查看快速鍵，但隨著使用的次數變多就能夠一想到要做什麼動作手就自動反應對應按鍵，寫 code 速度就會變快囉。
   
---


## 同場加映：英打練起來

除了快速鍵的手感之外，英打的準確度是更重要的！自己寫 code 還滿常踩到打錯字的雷。  
若你英打還不夠快、不夠準的話，每天睡前腦袋放空讓手練一波 ( 5-10 分鐘就好了 ) 。  
推薦六角學院開發的線上英打練習[ Keybr ](https://www.keybr.com/)，針對練習過程中的錯字機率去加強特定的字母練習：

![](https://i.imgur.com/bfbk62s.png)

傳送門：[Keybr](https://www.keybr.com/)｜[詳細介紹與教學](https://medium.com/@gonsakon/%E9%AB%98%E6%95%88%E7%B7%B4%E8%8B%B1%E6%89%93%E7%A5%9E%E5%99%A8-keybr-com-3cad9325a5e6)

--- 

邊寫code邊搭配著快速鍵慢慢把手感練起來吧！  
[下一篇](https://)將介紹個人常用的 VS Code 插件，使開發過程更加便利！

---

⮩ 本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10237385)
