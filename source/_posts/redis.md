---
title: 認識 Redis
date: 2019-04-13 11:18:37
tags:
  - redis
categories:
  - DB
---

## What is Redis?

Redis 為「快取資料庫」，為一個 in-memory 的 key-value database。in-memory 的意思是將 data 先存在 memory 上，之後再逐步或關機一次將 data 存入後端資料庫中，可以減輕後端資料庫面臨短時間湧入大量 data 的負擔。

## 優點

1.可避免尋找時間延遲，因為資料都放在 server 的 memory 上，不須再去磁碟或 SSD 上處理  
2.簡易指令即可存取 DB 的資料。

## 適用時機舉例

1111 購物節限時搶購優惠，因為在 1 秒內可能會湧入及大量的資料，因為通常後端資料庫都是將 data 存放在磁碟或 SSD 上，短時間大量資料會導致整個 DB 不堪負荷而掛掉。
