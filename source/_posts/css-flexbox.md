---
title: Flexbox
date: 2018-08-16 15:43:07
tags:
  - flexbox
categories:
  - CSS
---

![](/images/flexbox.png)

**Flex container**

- `display` : `flex`(就是`block-flex`) 或是 `inline-flex`
- `flex-direction` : 定義 Flex item 在 container 中的方向
  default : `row` (由左至右) => 1 2 3 4 5
  `row-reverse`(右至左) => 15 4 3 2 1
- `flex-wrap` : `wrap` 當螢幕變小會換行
- `flex-flow` : `<flex-direction>` `<flex-wrap>`
- `justify-content` : 在 main axis 中，定義 item 的排列
  `flex-start`,`flex-end`,`center`,`space-around`,`space-between`
- `align-items` : 在 cross axis 中，定義 item 的排列
  default : `stretch` => 根據 height 延伸
  `baseline` : 第一個字母的底線，會讓所有 item 即使 height 不等高，字也會在同一個高度
- `align-content` : 適用於有好幾個 row 或 column 時

**Flex item**

- `order` : 可改變順序，default 為`0`
- `flex-grow` : 可設定 grow 多少倍去填滿空白處，default 為`0`(不 grow)。
  可以一次將所有的 item 設定 grow，讓全部等長填滿。也可以單獨設定某幾個 item。
- `flex-shrink` : default 為`1`，即原本就有 shrink，只是到某種程度仍會換行。
  shrink = 0 => 不 shrink
  shrink = 4 => shrink 快 4 倍
- `flex-basis` : 決定 item 的 width。 `auto` => 根據內文決定 width
- `flex` : `flex-grow` `flex-shrink` `flex-basis`
- `align-self` : 個別排列 item， default 為`auto` => 看 container 對 `align-item`的設定
