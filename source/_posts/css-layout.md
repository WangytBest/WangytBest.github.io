---
layout: post
title: CSS实现元素水平垂直居中
date: 2017-09-13 16:14:28
tags: [CSS, CSS3]
categories: CSS
thumbnail: http://ow9cw9x3t.bkt.clouddn.com/spider-man.jpg
top: true
---

在前端开发过程中，盒子居中是常常用到的。其中 ，居中又可以分为水平居中和垂直居中。块级元素的水平居中比较容易，直接设置元素的```margin: 0 auto```就可以实现，垂直居中相对来说是比较复杂一些的。

## 高度位置，使用绝对定位

```css
.parentElem {
  position: relative;
}

.childElem {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
```

### 父容器高度已知

> 且只有一个元素，只要使用相对定位即可

```css
.parentElem {
  height: 200px;
}

.childElem {
  position: relative;
  top: 50%;
  transform: translateY(-50%);
}
```

## 水平居中方案
### 行内元素
```css
  text-aligin: center;
```
### 块级元素，宽度固定
```css
  margin: 0 auto;
```
### 块级元素，宽度不定
```css
  margin: 0 auto;
```

### vertical-align 垂直对齐

> 1. 元素默认垂直对齐方式为基准对齐（baseline）
> 2. 继承性： 不继承
> 3. **<font color="#DC143C">适用于行内元素和单元格（table-cell）元素</font>**

#### 语法

> * ```baseline``` : 基准线
> * ```middle``` : 中部对齐
> * ```top``` : 顶端对齐
> * ```bottom``` : 底端对齐
> * ```text-top``` : 与文本顶部对齐
> * ```text-bottom``` : 与文本底部对齐
> * ```sub``` : 下标
> * ```super``` : 上标
> * ```<百分比>```，```<长度>``` : 可为负数
> * ```inherit```

![垂直对齐属性](http://ow9cw9x3t.bkt.clouddn.com/vertial-align.gif)

图片本身没有基线，则将其底部与父元素的基线对齐。

[参考：垂直对齐：vertical-align属性](http://www.ddcat.net/blog/?p=233#)



