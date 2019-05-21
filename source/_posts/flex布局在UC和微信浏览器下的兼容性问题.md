---
title: flex布局在UC和微信浏览器下的兼容性问题
date: 2018-04-03 19:56:59
categories: [CSS]
tags: [CSS]
---

## flex布局

## UC和微信浏览器下的兼容性问题

所有`webkit`内核的浏览器（包括移动端）都支持 `flex` 布局，只不过一些浏览器只支持旧语法，如：`display: -webkit-box` 。
旧语法和标准的 `flex` 语法有较大区别，需要做好兼容。不过可以来使用 `autoprefixer` 来自动处理这些兼容性问题，而开发时只需要写标准的语法就好了。

假如没有使用`autoprefixer`，在UC浏览器和微信内置浏览器中，使用`display:flex;`时会不起作用，要加上兼容性写法。
<!-- more -->
```css
display: -webkit-box;      /* OLD - iOS 6-, Safari 3.1-6 */
display: -moz-box;         /* OLD - Firefox 19- (buggy but mostly works) */
display: -ms-flexbox;      /* TWEENER - IE 10 */
display: -webkit-flex;     /* NEW - Chrome */
display: flex;
```

使用`flex:1;`时也要添加兼容性写法
```css
           width: 20%;       /* For old syntax, otherwise collapses. */
-webkit-box-flex: 1;         /* OLD - iOS 6-, Safari 3.1-6 */
   -moz-box-flex: 1;         /* OLD - Firefox 19- */
    -webkit-flex: 1;         /* Chrome */
        -ms-flex: 1;         /* IE 10 */
            flex: 1;  
``` 

[flex.css](https://github.com/lzxb/flex.css)