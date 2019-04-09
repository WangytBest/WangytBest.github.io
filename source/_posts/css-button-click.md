---
title: 按钮点击水波效果
date: 2017-09-25 16:42:20
tags: [css, button, canvas]
categories: [CSS]
# thumbnail: http://cloud.xuww.wang/nianshaodeni.png
---

Material Design设计按钮点击效果比较酷炫，每次点击按钮都会产生一次水波涟漪的效果。

可以css和canvas来实现这种效果。
<!-- more -->
### css实现

伪类（pseudo-class）和伪元素(peseudo-element)

#### 伪类
> * ```:before```
> * ```:after```

#### 链接定义样式
> * ```:hover``` : 鼠标滑过元素上方时的展现效果
> * ```:active``` : 鼠标单击元素时展现效果
> * ```:visited``` : 已经单击过的链接
> * ```:link``` : 未访问、未滑过、未点击过的链接标签的样式

#### 段落样式
> * ```:first-letter``` : 首字母
> * ```:first-line``` : 首行

#### 设置元素

> button元素在没有点击或者鼠标滑过时设置按钮样式,同时设置hover和active的样式效果

```css
.button {
    text-decoration:none;
    user-select:none;
    position: relative;
    display: block;
    margin: 100px auto;
    width:120px;
    height:50px;
    line-height:50px;
    text-align:center;
    border-radius:25px;
    border: none;
    color:#fff;
    font-size:16px;
    cursor:pointer;
    background-color: #ff8300;
    box-shadow: 0 3px 9px 0 rgba(255, 131, 0, 0.35);
    overflow: hidden;
}

.button:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 13px 0 rgba(255, 131, 0, 0.59);
}

.button:active {
    box-shadow: 0 3px 9px 0 rgba(255, 131, 0, 0.35);
    color: #ffca8c;
    background-color: #f07b00;
    transform: translateY(0);
}
```
<script async src="//jsfiddle.net/wangyutao/3vseL19b/2/embed/html,css,result/"></script>

> 添加水波效果




** 参考 **
![](http://cloud.xuww.wang/click-button.png)



