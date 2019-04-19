---
title: css中position属性深入探讨
toc: true
tags: [CSS]
categories: [CSS]
date: 2019-04-11 10:58:22
thumbnail:
---

对于 `position` 属性可以说是平时开发中使用频率非常高的 `CSS` 属性，本文主要对 `position` 做个总结。

`position` 属性能够很好的体现 HTML 的普通流的特征。设置 `position` 属性之后主要关注**是否脱离文档流**和**改变 `display` 属性**

> `position`: `static` | `relative` | `absolute` | `sticky`

<!-- more -->

## static

所有元素在默认情况下 `position` 属性值都为 `static` ，此时设置`top`、`left`、`bottom`和 `right` 在 `position` 为 `static` 的情况下无效。
用法：在改变了元素的 `position` 属性后可以将其元素重置为 `static` ，让其回归到正常的普通文档流中。

## relative

相对定位: 指给元素设置相对于原本位置的定位，元素并不脱离文档流，因此元素原本的位置会被保留，其他的元素位置不会受到影响。

每个元素在页面中的普通流中都会占用一个位置（元素默认文档流位置），设置为相对定位后，将元素偏离元素的默认位置，但是普通文档流中依然保持着原有的默认位置，并没有脱离普通文档流。

### 块级元素

```html
<style type="text/css">
  div{ 
    width: 100px; 
    height: 50px; 
    line-height: 50px; 
    text-align: center; 
    color: #fff; 
  }

  div .A {
    background: blue;
  }

  div .B {
    background: red; 
    position: relative; 
    top: 20px; 
    left: 20px;
  }
  div .C {
    background: green;
  }
</style>
<div class="A">A</div>
<div class="B">B</div>
<div class="C">C</div>
```
![相对定位](http://blog.cloud.xuww.wang/position-relative-block.png)

在右图中的黑色虚线部分为B块的默认文档流位置，当B块设置为相对定位 `relative` 之后，则相对于**默认位置**进行偏移。C块依然保留在原位，并没有因为B块发生了偏移而随之变化。

### 行内元素

```html
<style type="text/css">
  strong { 
    background: #808080; 
  }
  em { 
    background: #ffd800; 
  }
  span { 
    background: #b6ff00; 
    position: relative; 
    top: 10px; 
    left: 10px; 
    width: 100px;
  }
</style>

<strong>strong</strong>
<em>em</em>
<span>span</span>
```

![行内元素-相对定位](http://blog.cloud.xuww.wang/position-relative-inline.png.png)

行内元素在设置 `relative` 之后，依然是内联元素， `widht` 属性未生效，并**没有改变行内元素的display属性**（这是与 `absolute` 的一个重要的区别）。

## absolute

绝对定位: 是指给元素设置绝对的定位，相对定位的对象可以分为两种情况：
1. 设置了 `absolute` 的元素如果存在有祖先元素设置了 `position` 属性为 `relative` 或者 `absolute` ，则这时元素的定位对象为此已设置 `position` 属性的祖先元素。
2. 如果并没有设置了 `position` 属性的祖先元素，则此时相对于 `body` 进行定位。

`position: absolute`相对于第一个不是 `static` 的父级元素进行定位。如果在其节点中所有的父级祖先元素都没有设置 `position` 属性为 `relative` 或 `absolute` 则该元素最终将对 `body` 进行位置偏移。

> 设置绝对定位的元素会**脱离普通的文档流**并且**改变diaplay属性**。

结论：
* 块级元素在设置为absolute绝对定位之后，会将width设置为auto（收到父元素的影响）
* 行内元素在设置为absolute绝对定位之后，如果没有设置其top、left、bottom和right属性的话，浏览器会设置成auto，auto的值则是该元素的默认位置。

## relative|absolute 点

1. 应用了`position: relative | absolute`的元素，`margin`属性依然生效，尽量不要设置`margin`，减少干扰、不精确。
2. `position: absolute` 将会忽略根元素的padding。
3. 行内元素使用了`position: absolute`之后会改变`display`属性，`inline-block`。
4. 设置`position: relative | absolute`之后，会覆盖其他非定位的元素，如果不想覆盖其他元素，也可以将其`z-index: -1`。

## fixed

绝对定位。
* 改变行内元素的`display`属性，使其`display`属性变更为`block`。
* 会让元素脱硫文档流，不占据空间
* 覆盖在非定位元素

`fixed` 和 `absolute` 的区别： `absolute` 根据第一个不是 `static` 的父元素进行定位， `fixed` 是根据浏览器窗口定位。

## sticky

粘性定位: `sticky` 的元素，在屏幕范围（`viewport`）时该元素的位置并不受到定位影响（设置是 `top` 、 `left` 等属性无效），当该元素的位置将要移出偏移范围时，定位又会变成 `fixed` ，根据设置的 `left` 、 `top` 等属性成固定位置的效果。

可以知道sticky属性有以下几个特点：

* 该元素并不脱离文档流，仍然保留元素原本在文档流中的位置。
* 当元素在容器中被滚动超过指定的偏移值时，元素在容器内固定在指定位置。亦即如果你设置了top: 50px，那么在sticky元素到达距离相对定位的元素顶部50px的位置时固定，不再向上移动。
* 元素固定的相对偏移是相对于离它最近的具有滚动框的祖先元素，如果祖先元素都不可以滚动，那么是相对于viewport来计算元素的偏移量

## position和float

1. 当元素同时设置 `position: relative` 和 `float: left` ，则元素先浮动到相应的位置，然后在根据 `top/ left / bottom / right` 来发生偏移。
2. 当元素同时设置 `position: absolute` 和 `float: left` ，则 `float` 失效。
