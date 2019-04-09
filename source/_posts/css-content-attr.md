---
title: CSS中的content和attr
date: 2017-09-15 16:37:47
tags: CSS
categories: CSS
toc: true
# thumbnail: http://cloud.xuww.wang/nianshaodeni.png
---

content和attr表达式，它们能在你的页面下面悄悄的使用CSS来生成内容，下面让我们看看attr和content如何相互配合产生神奇效果的。

### 基本content用法

> content属性能让程序员使用CSS往页面元素里填写内容：

```css
.myDiv:after {
    content: "我是一个使用*content*属性生产的静态文字"; 
}
 ```

<!-- more -->
请注意，如果想让伪元素```:after```绝对定位，你必须对你的div设置```position: relative```。

### content和attr配合使用

如果你不想把content内容在CSS里写死，那你可以使用attr表达式来从页面元素中动态的获取内容：
> attr属性通常和自定义属性data-配合使用，因为传统的其它属性虽然也能存值，但通常不适合存放表达性文字。

```css
/* <div data-line="1"></div> */
div[data-line]:after {
    content: attr(data-line); /* 属性名称上不要加引号！ */
}
```

### content里的字符串连接操作

> content内容支持字符串的拼接

这种字符串连接很像常规编程语言了：

```css
/* <div data-line="1"></div> */
div[data-line]:after {
    content: "[line " attr(data-line) "]";
}
```
还需要用JavaScript里拼装字符串吗？CSS3里就能完成这些，是不是感觉CSS3可以部分的替代Javascript了！attr的动态生成页面内容的能力着实是一件让人兴奋的事情。你实际上可以用它配合content对页面的很多其他元素和属性进行操作。