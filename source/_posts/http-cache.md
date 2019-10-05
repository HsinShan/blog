---
title: Http Cache
date: 2019-09-30 11:12:12
tags:
  - Cache
  - HTTP
categories:
  - 計算機概論
---

之前有篇文章 {%post_link http%} 有稍微提到 Cache 的概念，但因為還是不太其運作方式及實際運用，所以決定重新研究一下。
參考文章：[循序漸進理解 HTTP Cache 機制](https://blog.techbridge.cc/2017/06/17/cache-introduction/)

## What is Cache?

在{%post_link http%} 有提到 cache 由 HTTP 控制，可以自動將資源副本保存在 local 端，減少 client-server 端的通信次數，不但可以加速頁面載入，也可以減少網路延遲。
常用於將**不常變動或短期內不會變動**的資料儲存起來，避免每一次訪問都要再去資料庫重新抓一次所有的資料，在電商網站中可以大大地減輕資料庫的負擔

## Server side Cache

將資料庫中的資料抓出來存到別的地方  
例如：redis(快取資料庫)，是一個 in-memory 的 key-value 資料庫，可參考之前的文章 {%post_link redis%}

## 有關 Cache 的過期設定

1.`Expires` : 在 http header 中，加入 Expires 可設定 cache 到期的時間  
2.`cache-control & max-age`: `Cache-Control: max-age=30` 即代表 cache 的過期時間為 30 秒  
注意：當上面兩個指令同時使用時，**優先看 cache-control & max-age**

## 運作流程

browser get server response  
-> cache -> 再度造訪  
-> check 現在時間是否到期( freshness)  
-> 若未到期則不發送 request，而是直接拿電腦裡已存好的 cache 資料

## 如果 cache 過期然後呢？

過期**不代表原本緩存的資料就不能用**，可透過檢查資料是否被更新，來決定要不要重新發送 request  
1.看 `Last-Modified` 與 `If-Modified-Since`  
2.看`Etag` 跟 `If-None-Match`

## 何時不要 cache ?

**當含有機密資料的時候**
方式： 指定 `max-age` 或是使用 `Cache-Control: no-store`

## 電商網站如何使用 Cache?

目的： 把頁面快取起來，但只要首頁一變動，就能夠立刻看到新的頁面
方法一： `Cache-Control: max-age=0` ＋ `Etag`  
方法二： `Cache-Control: no-cache`

## 注意

no-cache：**永遠檢查快取**，會發送 request 檢查資料有沒有更新
no-store：永遠不用快取
