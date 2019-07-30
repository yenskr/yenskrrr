---
title: 如何在win10中解壓縮tar檔案
author: Yenskr
date: '2019-07-29'
slug: extract-tar-file-on-win10
categories:
  - System
tags:
  - tar
  - linux
  - win10
  - cmd
images: []
---

### 前言
當我們把程式更新推送到 [shinyapps.io](https://www.shinyapps.io/admin/#/dashboard)，會把舊的檔案蓋掉。如果想要在推送前把舊版檔案備份的話，可以先到 shinyapps.io 把專案的 bundle 整個下載下來。  

![bundle](https://i.imgur.com/URIEair.jpg)

從 <kbd>shinyapps.io</kbd> 下載下來的 <kbd>bundle</kbd> 檔案是 <kbd>.tar</kbd> 格式，如果直接用 <kbd>rar</kbd> 軟體，解壓縮出來的東西是看不懂的...  

![](https://i.imgur.com/3bKGnFE.jpg)

---

### 問題
> 在win10環境下成功解壓縮 <kbd>.tar</kbd> 檔案

### 解法

1. 使用 <kbd>cmd</kbd> 或 <kbd>powershell</kbd> 等工具打開命令列(個人使用 [ConEmu](https://conemu.github.io/)，推薦！)，用 <kbd>tar</kbd> 指令解壓縮。
2. 輸入下列指令及參數
{{< highlight cmd >}}> tar -xvzf [檔案路徑/file.tar] -C [解壓路徑資料夾]
{{< /highlight >}}
3. 參數說明:
    - x — 表示指定模式為「解壓縮」，**必要參數**。(其他模式尚有`-c`、`-r`、`-t`、`-u`)
    - v — verbose. 顯示詳細解壓縮過程，**非必要參數**。
    - z — tells tar to uncompressed the content of a .tar.gz file with gzip.
    - f — instructs tar the name of the file you’re about to extract. 
    - C - 更換至[解壓路徑資料夾]。(Change to \<dir\> before processing remaining files)
    - `cmd` 中輸入 `tar --help` 看更多參數說明
    
4. 解壓縮成功!
![](https://i.imgur.com/JAz2pmV.jpg)

### 參考
- https://support.rstudio.com/hc/en-us/articles/204536588-Downloading-your-application-from-shinyapps-io
- https://pureinfotech.com/extract-tar-gz-files-windows-10/
- https://anal02.pixnet.net/blog/post/113556857-tar%E8%A7%A3%E5%A3%93%E7%B8%AE%E6%8C%87%E4%BB%A4

###### tags: `tar` `win10` `linux` `cmd`