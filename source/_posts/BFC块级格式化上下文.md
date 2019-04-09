---
title: BFC块级格式化上下文
toc: true
categories: [CSS]
date: 2019-04-09 15:51:52
tags: CSS
thumbnail:
---

## BFC（Block Formating Context）
> 块级格式化上下文：一个独立的渲染区域，只有`Block-level box`参与，它内部规定了`Block-level box`如何布局，并且与这个区域外部毫不相干。

#### BFC布局规则
* 内部`Box`会在垂直方向上一个接一个的放置
* `Box`垂直方向的距离由`margin`决定。属于同一个`BFC`的两个相邻`Box`的`margin`会合并
* 每个元素的`margin box`的左边，与包含块`border box`的左边相接触
* `BFC`的区域不会与`float box`重叠
* `BFC`是一个独立的容器，里面的子元素不会影响到外面的元素，反之亦然。
* 计算`BFC`的高度的时候，浮动元素也参与计算

<!-- more -->

#### 生成BFC
* 根元素
* `float`属性不为`none`
* 绝对定位元素（`absolute`, `fixed`）
* `display`为`inline-block`,`table-cell`,`table-caption`,`flex`, `grid`
* `overflow`不为`visible`

#### BFC作用
1. 自适应两栏布局
2. 可以阻止元素被浮动元素覆盖
```html
<html lang="en">
<head>
</head>
<body>
  <div class="aside"></div>
  <div class="main"></div>
</body>
</html>
```
```css
body{
  width: 300px;
  position: relative;
}
.aside {
  width: 100px;
  height: 150px;
  float: left;
  background: #f66;
}
.main {
  height: 200px;
  background: #fcc;
  overflow: hidden;
}
```

`main`节点如果不设置为`BFC`，那么根据规则每个元素的`margin box`的左边，与包含块`border box`的左边相接触,`main`将会被`aside`覆盖。通过`overflow:hidden`设置为`BFC`，`BFC`区域不会和`float box`重叠。

3. 可以包含浮动元素——清除内部浮动
> 包含浮动元素的父元素，设置 `overflow: auto` 创建一个新的BFC来包含这个浮动。父元素现在变成布局中的迷你布局，任何子元素都会被包含进去。

4. 分属于不同的BFC时可以阻止margin重叠
> 外边距塌陷: 创建新的BFC避免两个相邻`<div>`之间的外边距合并

## 外边距塌陷

> 外边距折叠：块级元素的上外边距和下外边距有时会合并（或折叠）为一个外边距，其大小取其中的最大者。

**注意浮动元素和绝对定位元素的外边距不会折叠**。

#### 外边距折叠的三种基本情况

##### 1. 相邻元素之间
毗邻的两个元素之间的外边距会折叠（除非后一个元素需要清除之前的浮动）。

##### 2. 父元素与其第一个或最后一个子元素之间

如果在父元素与其第一个子元素之间不存在边框、内边距、行内内容，也没有创建块格式化上下文、或者清除浮动将两者的`margin-top`分开；或者在父元素与其最后一个子元素之间不存在边框、内边距、行内内容、`height`、`min-height`、`max-height`将两者的`margin-bottom`分开，那么这两对外边距之间会产生折叠。此时子元素的外边距会“溢出”到父元素的外面。

##### 3.空的块级元素
如果一个块级元素中不包含任何内容，并且在其`margin-top`与`margin-bottom` 之间没有边框、内边距、行内内容、`height`、`min-height`将两者分开，则该元素的上下外边距会折叠。

#### 一些需要注意的地方：

* 上述情况的组合会产生更复杂的外边距折叠。
* 即使某一外边距为0，这些规则仍然适用。因此就算父元素的外边距是0，第* 一个或最后一个子元素的外边距仍然会“溢出”到父元素的外面。
* 如果参与折叠的外边距中包含负值，折叠后的外边距的值为最大的正边距与最小的负边距（即绝对值最大的负边距）的和。
* 如果所有参与折叠的外边距都为负，折叠后的外边距的值为最小的负边距的值。这一规则适用于相邻元素和嵌套元素。

[MDN: BFC 块级格式化上下文](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

