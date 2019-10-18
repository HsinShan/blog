---
title: 淺談 Virtual DOM
date: 2019-08-26 16:28:21
tags:
  - Virtual DOM
categories:
  - Frontend
---

## What is Virtual DOM?

使用 Javascript 的物件構成的樹狀 Virtual DOM，用來模擬真實的 DOM，所以和 DOM 有一一對應的關係，目前 react 跟 vue 皆使用 Virtual DOM。
Virtual DOM 至少含有３個屬性，分別為 tag、props、children，在不同框架屬性名可能不同。

    {
      tag: 'div',
      props: [ { 'id': 'childId' } ],
      children: [
        {
          tag: 'div',
          props: [],
          children: [
            {
              tag: 'div',
              props: [],
              children: [...]
            }
          ]
        },
        {
          tag: 'div',
          props: [],
          children: [...]
        }
      ]
    }

而 Vue 的 Virtual DOM 即為 vNode!!

## Why Virtual DOM?

目的：**不直接操作 DOM**，因為成本太高了！！

#### Performance(頁面渲染的性能分析)

一般透過 chrome dev tool 可看出頁面渲染時，至少會經過四個階段
**Loading(HTML 解析) -> Scripting(JS 運算)-> Rendering(生成渲染樹) -> Painting(繪製頁面)**
在選擇直接操作 DOM ，則每次更動都必須重新執行上面的流程，當頁面越趨複雜且龐大時，Rendering 和 Painting 所需的時間就會越來越長，且每次稍微更動就須重新渲染，也會大大降低效能。

因此，若使用 Virtual DOM，則可解決此問題．

#### Virtual DOM 的運作流程

不直接操作 DOM 改為操作 Javascript 物件。
**操作 Javascript 物件 -> 形成 Virtual DOM -> 在內存進行更新前後的 Virtual DOM 比較 -> 依據各框架設定在指定時機更新真實的 DOM**

#### Advantage

1. 減少渲染次數，提高渲染效率 -> **效能 up up**
   (但並非效能總是會比直接操作 DOM 來得好)
2. 因為頁面狀態為抽象的 JS 物件，所以搭配不同渲染工具，可以達到**跨平台渲染**的作用

更多相關好文推薦：[Virtual DOM 概述](https://cythilya.github.io/2017/03/31/virtual-dom/)、[你不知道的 Virtual DOM（一）：Virtual Dom 介绍](https://segmentfault.com/a/1190000016129036)

**2019/10/18 更新**
延伸好文推薦：[深度剖析：如何实现一个 Virtual DOM 算法](https://github.com/livoras/blog/issues/13#)
