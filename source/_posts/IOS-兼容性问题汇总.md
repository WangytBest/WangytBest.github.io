---
title: IOS 兼容性问题汇总
toc: true
tags: []
categories: []
keywords: []
date: 2019-06-17 15:38:21
thumbnail:
---

1. iOS 某些情况下字体放大 
  使用 `-webkit-text-size-adjust: 100% !important;`解决

2. iOS 
  `-webkit-overflow-scrolling: auto !important;` 解决iOS部分手机滚动部分区域白块现象

3. 页面元素高度等于行高，文字却没有垂直居中，表现为ios上和浏览器上能很好的垂直居中，安卓端的文字明显偏上
  * 不要设置`height` ，`line-height` 设置为1，用padding值上下相等来保持垂直居中
  * 通过 `transform` ，放大一倍再缩小一半（写起来繁琐而且影响布局，这个是有效果的）

  