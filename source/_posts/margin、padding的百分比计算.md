---
title: margin、padding的百分比计算
date: 2018-04-20 10:54:12
categories: [CSS]
tags: CSS
---
### CSS2.1 Box model

> The percentage is calculated with respect to the width of the generated box’s containing block. Note that this is true for `margin-top` and `margin-bottom` as well.

margin：百分比的计算基于生成框的包含块(父元素)的width（margin-top/bottom也是如此）。
padding同理