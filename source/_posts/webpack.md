---
title: 前端自動化工具--淺談 Webpack
date: 2019-06-03 23:10:31
tags:
  - webpack
  - Vue cli
catogories:
  - Frontend
---
## What is Webpack?
Module bundler(靜態模塊打包工具)，他將所有東西(CSS、JS、image...)都是為模塊，自動編譯成瀏覽器看得懂的東西，讓我們可以專心去處理 preprocess(前處理，像是 ES6、pug、sass、Vue、React)的部分。
我們前處理的東西都會放在 src 資料夾下，而 webpack 編譯的東西都會放在 dist 資料夾下

## webpack的核心概念1-> import (注入)
我們會將所需的所有東西 import 進去進入點(`index.js`)，也就是在 `webpack.config.js` 中設定好的 entry 檔

``` javascript
const path = require('path');
module.exports = {
    entry: './index.js',
    output: {
        filename: 'index.bundle.js',
        path: path.resolve(__dirname, './'),
    }
};
```

`package.json`：關於這整包專案所有的資訊，包含此專案所安裝的套件版本、專案版本及 npm 指令，每次只需執行 `npm install`就會依照此檔案安裝所需套件
`package-lock.json`：`package-lock.json`是 npm5 版本新增的，和`Yarn.lock`類似，是專門紀錄 `package.json` 裡面更細節的內容，例如安裝的套件的詳細版本，或是確認你的dependency(依賴)是被哪個函式庫所要求的等等，因為若很多事後再版本更新時，很容易因為一些改動，就造成專案跑不動，所以要補足`package.json`可能沒記錄到的地方，因而新增此檔案，不過檔案通常就放著不太會管它。

## webpack的核心概念2-> Code Splitting 
webpack 有別於傳統的模塊打包工具，它可以將程式碼分割成多個獨立的模塊，再依需要的優先順序加載，若使用得當，可以減少首次載入所需時間

**Vue CLI (Command Line Interface)為快速建置vue專案的工具，為vue.js官方提供的開發工具，vue-cli 會讓我們選擇要裝的webpack**

參考好文：[Webpack教學 (一) ：什麼是Webpack? 能吃嗎？](https://medium.com/@Mike_Cheng1208/%E4%BB%80%E9%BA%BC%E6%98%AFwebpack-%E4%BD%A0%E9%9C%80%E8%A6%81webpack%E5%97%8E-2d8f9658241d)

## Webpack4 新活動
1. 支持將近 93% 的 ES6 的語法
2. 不再强制以 `webpack.config.js` 作为打包的入口配置文件了！
它會自動默認入口為 `./src/` 和默認出口 `./dist`，利於小專案的快速建置
3. 新增 mode 選項，可選擇 production 或 development，讓 webpack 知道所處模式並進行內置優化
