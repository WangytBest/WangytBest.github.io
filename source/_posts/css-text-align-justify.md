---
title: css文字两端对齐
date: 2017-10-16 14:37:17
categories: [CSS]
tags: CSS
# thumbnail: http://cloud.xuww.wang/nianshaodeni.png
---

文本内容可以实现左对齐、右对齐以及居中对齐，如何实现两端对齐？很多时候为了对齐文字中间使用空格来隔开，这样每个内容需要计算空格个数，当内容不一样长短的时候又通过JS进行麻烦的计算。

`text-align`是控制文字的对齐与显示，从其属性名上就可以看出来。从其渲染与解析上来看，其主要是用来控制`inline`水平元素或`inline-block`元素的对齐与显示的，例如嵌套行内标签的文字、图片、input表单控件等；而对block水平的元素是没有作用的。

```css
text-align: center | left | right | start | end | justify | inherit | initial | unset
text-align: justify
```
css2中`text-align`有一个属性为`justify`，居中对齐。其实现的效果就是可以让一行文字两端对齐显示（文字内容要超过一行）
<!-- more -->
* 有多行文字
> 多行文字内容时直接使用`justify`可以实现两端对齐效果

```html
<div>Vue.js (读音 /vjuː/，类似于 view) 是一套构建用户界面的渐进式框架。与其他重量级框架不同的是，Vue 采用自底向上增量开发的设计。Vue 的核心库只关注视图层，它不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与单文件组件和 Vue 生态系统支持的库结合使用时，Vue 也完全能够为复杂的单页应用程序提供驱动。</div>
```
```css
div {
    width: 500px;
    border: 1px solid #000;
    text-align: justify;
}
```

* 只有一行文字

> 需要在文字后面加一个占位元素，可以使用伪类元素实现，或者加`<span></span>`、`<i></i>`空元素。

```html
<div>css文字两端对齐！</div>
```
```css
div {
    width: 500px;
    border: 1px solid #000;
    text-align: justify;
}
```

此时的效果并没有实现两端对齐，因为文字内容没有换行。可以使用伪类元素实现。
```css
div {
    width: 500px;
    border: 1px solid #000;
    text-align: justify;
}
div:after {
    content: '';   
    display: inline-block;
    width: 100%;
}
```

