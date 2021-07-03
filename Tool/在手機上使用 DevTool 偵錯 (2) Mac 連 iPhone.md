---
title: '[DevTool] 行動開發-Mac 連至 iPhone 裝置進行校調 (Safari Web Inspector )'
tags: [DevTool, iOS, Safari, deBug]
category: DevTool
date: 2021-05-31 20:06:42
permalink: posts/210531

---

對 iOS 行動裝置（本例為 iPhone） 開啟 Safari Web Inspector (網頁檢閱器) 操作的設定步驟。

<!--more--> 

> 適用需求:  
> - Mac 開發、需要即時在 iOS 行動裝置上瀏覽畫面並直接使用 Safari Inspector 操作。
  
---

## Step 1. Safari 設定

### Mac 的 Safari :

- "Safari" -> “偏好設定” -> "進階" -> 勾選“在選單列中顯示開發選單”

    <div style="max-width:240px;">

    ![Image](https://i.imgur.com/EMUk05V.png)

    </div>


    ![Image](https://i.imgur.com/B1gm29B.png)


### iPhone 的 Safari：

- "設定" -> "Safari" -> “進階” -> 開啟“網頁檢閱器”

    ![Image](https://i.imgur.com/1orxuVF.png)


## Step 2. iPhone Safari 瀏覽網頁


  <div style="max-width: 260px; margin: auto;">

  ![Image](https://i.imgur.com/MNaA2GL.png)

  </div>

- 若是要瀏覽(訪問) Mac 開發環境運行中的 Localhost，可參考：[讓手機瀏覽 Localhost](/posts/210529/)


## Step 3. iPhone 與 Mac 實體連接、開啟 Mac Safari

- 將 iPhone 透過 USB 線連接至 Mac

- (Mac) Safari "開發“ → "iPhone 名“ → 頁面

    <div style="max-width:550px; margin: auto;">

    ![Image](https://i.imgur.com/jctTOVq.png)

    </div>

    

即可直接對手機上的頁面使用 Web Inspector。