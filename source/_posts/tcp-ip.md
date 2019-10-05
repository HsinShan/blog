---
title: TCP/IP
tags:
  - IP
  - MAC
  - TCP
url: 243.html
id: 243
categories:
  - 計算機概論
date: 2019-04-27 14:23:22
---

(2019/10/04 更新)

## What is OSI?

參考資料：[什麼是 OSI 的 7 層架構？和常聽到的 Layer 7 有關？](https://ithelp.ithome.com.tw/articles/10000021)
OSI，是由國際化標準組織（ISO）針對開放式網路架構所制定的電腦互連標準，全名是「開放式通訊系統互連參考模型」（Open System Interconnection Reference Model），簡稱 OSI 模型。
依據網路運作方式，OSI 模型共切分成 7 個不同的層級，每級按照網路傳輸的模式，定義所屬的規範及標準。由具體到抽象的網路傳輸方式層次來看，7 層分別為實體層、資料連結層、網路層、傳輸層、會議層、展示層及應用層。

## What is 通訊協議(Protocol)?

通訊協議是在計算機連間之間，必須遵守的協議準則。

## What is TCP?

屬於 OSI 7 層中的傳輸層
TCP（Transmission Control Protocol)，只要符合 TCP 所制定的規則，TCP 就會**保證資料收發必定正常**。
因為 TCP 協定在傳輸一開始，會有**三次握手（Three-way handshake）**的機制，來確保雙方資料收發都是正常的。

## What is UDP?

屬於 OSI 7 層中的傳輸層
UDP（User Datagram Protocol)，只要符合 UDP 所制定的規則，UDP 就會**保證資料傳遞的即時性**，效能較佳。
常用於視訊、直播等

## What is IP?

屬於 OSI 7 層中的網路層
IP (Internet Protocol):也為一種協定，為實際傳遞資料時，記錄資料收發地址（IP 地址）的協定

**IP 位址**: 互聯網協議地址，由協議派給每台主機的數字標籤，因 IP 位址可達成數據傳送之目的。 子網路遮罩(以 255 開頭):用來標示 IP 位址所在的子網。 IP 位只有分 IPv4 和 IPv6，是因為 IPv4 數量有限。
**MAC 地址**:  網卡的物理位置、硬體地址或鏈路地址，由網絡設備製造商生產時寫在硬體內部，與網路無關。(屬於 OSI 7 層中的資料連結層)
