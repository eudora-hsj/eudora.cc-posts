---
title: '[DevTool] 行動開發-讓手機瀏覽(訪問)開發環境的 Localhost (Mac / Windows)'
tags: [devTool, deBug, localhost]
category: DevTool
date: 2021-05-30 20:06:42
permalink: posts/210530

---

在行動裝置上瀏覽開發環境運行的 Localhost。

<!--more--> 

> 適用需求:  
> - 本地開發運行 Local Server，需要於行動裝置上運行。
  
---
## 條件 & 原理

1. 開發環境與行動裝置須為同一區網。
2. 開發環境關閉網路防火牆、指定 Port 可開放連線。
3. 運行 LocalServer 並查詢本地 IP。
4. 行動裝置連線至開發環境 IP。

## Step1.連至同一個區網

- 確認當前電腦與手機處於同個網段

   例如連同一個 WiFi / 電腦連手機網路

## Step2.運行 Local Server

-  開發環境運行 Local Server (如：`localhost:8080`)

## Step3.防火牆設定 & IP 查詢

### Mac 設定

- Mac "設定" -> "安全性與隱私權" -> 關閉 防火牆

  ![Image](https://i.imgur.com/6UOTgta.png)
  
- 查詢 Mac IP 位址

    終端機輸入 ：`ifconfig` 



    <div style="max-width:500px; margin: auto;">

   ![Image](https://i.imgur.com/puwOEBY.png)

    </div>


    或直接在 "網路" 中查看 

   ![Image](https://i.imgur.com/Sb7ZCI4.png)

### Windows 設定

- Windows "控制台" -> "Windows Defender 防火牆" -> 開啟或關閉 Defender 防火牆  -> 關閉防火牆

   <div style="max-width:700px; margin: auto;">

   ![Image](https://i.imgur.com/L6D3je5.png)
   
   ![Image](https://i.imgur.com/rZJiPzO.png)

    </div>


- 查詢 IP 位址

    - `windows + R` 輸入 cmd 開啟命令提示字元
    - 輸入 `ipconfig`

      ![Image](https://i.imgur.com/SMS3GH2.png)

      ![Image](https://i.imgur.com/dy10oZB.png)

   - 或直接從網路連線中查詢 IP
  
      ![Image](https://i.imgur.com/mSOLc74.png)

---

## Step3. 在行動裝置上連至目標頁

- 如`192.168.XX.XX:8080`
   
  <div style="max-width: 300px; margin: auto;">

  ![Image](https://i.imgur.com/kmxc428.png)

  </div>
