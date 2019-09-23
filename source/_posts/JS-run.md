---
title: Javascript 的運作模式(未完待續)
date: 2019-09-16 11:37:06
tags:
  - JS-advanced
  - compile
  - RHS
  - LHS
categories:
  - Javascript
---

## 直譯式語言 v.s. 編譯式語言

以 Javascript 為例，他的原始碼是無法直接被電腦解讀的，所以在原始碼交付給電腦運行之間會需要“翻譯”的工具。而這所謂的翻譯工具有兩種，一種為直譯器，另一種為編譯器，而 Javascript 所使用的就是直譯器。

##### 直譯式語言 -- 使用直譯器

代表語言： Javascript、Python、Ruby 等

<img src="./直譯式語言.png" width = "70%" height = "auto" alt="直譯式語言" style="margin-left:0px;"/>圖片來源:六角學院課程

簡單來說，直譯式語言會使用直譯器(Interpreter)將原始碼直接一句一句翻譯並執行，當遇到錯誤時會直接反映在環境中 。
**優點** 1.不需事先定義型別 2.程式較為彈性

**缺點**
執行速度會比編譯式語言慢一點，但效能還是取決於直譯器本身

##### 直譯式語言 -- 使用編譯器

代表語言：C、C++、Objective-C、Visual Basic 等

<img src="./編譯式語言.png" width = "70%" height = "auto" alt="編譯式語言" style="margin-left:0px;"/>圖片來源:六角學院課程

編譯式語言在電腦執行前，會先將所有原始碼透過編譯器(Compiler)編譯(compile)成電腦看得懂的代碼再執行，所以當有錯誤時，在編譯時就會被發現，可以預先除錯。
**優點**
執行速度較快，因為在執行之前就被編譯好了

**缺點**
開發速度較慢，因為除錯時間較長
