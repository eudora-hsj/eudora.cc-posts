---
title: '[DevTool] 行動開發-Windows 連至 Android 裝置進行校調  (Chrome DevTools )'
tags: [DevTool, Android, Chrome, deBug]
category: DevTool
date: 2021-06-01 20:06:42
permalink: posts/210601

---

對 Android 行動裝置開啟 Chrome DevTools  (開發者工具) 操作的設定步驟。

<!--more--> 

> 適用需求:  
> - Windows 開發、需要即時在 Android 裝置上瀏覽畫面並直接使用 Chrome DevTools 操作。
  
---

## Step 1.Android 手機設定

### Android 開啟開發者模式 

- "設定" -> "關於/關於手機" (每個手機的字略有不同) -> “連續點 7 次” 後開啟"開發者模式"

    (ps. 不同型號手機開啟開發者模式的方式可能不同)

    ![Image](https://i.imgur.com/kRYEuOc.png)

- "設定" -> (多了) "開發人員選項" -> 開啟" USB 除錯" 

  <div style="max-width: 580px; margin: auto;">

    ![Image](https://i.imgur.com/Yxv2uye.png)
    
  </div>

## Step 2. Android Chrome 瀏覽網頁


  <div style="max-width: 260px; margin: auto;">

![Image](https://i.imgur.com/PaEtnT9.png)

  </div>


- 若是要瀏覽 Windows 開發環境運行中的 Localhost，可參考：[讓手機瀏覽(訪問) Localhost](/posts/210529/)

## Step 3. Android 與 Windows 實體連接、開啟 Windows Chrome

- 將 Android 手機透過 USB 線連接至 Windows

- Chrome 連至 `chrome://inspect/#devices`
- 選定目標網頁或輸入網址開啟


    <div style="max-width:550px; margin: auto;">


    ![Image](https://i.imgur.com/Ud3b0ab.png)


    </div>

即可直接對手機上的頁面操作 Chrome DevTools。