---
title: JS原生图片懒加载
date: 2017-09-20 14:43:41
tags: [Javascript, 图片, 懒加载， 原生JS]
categories: Javascript
thumbnail: http://ow9cw9x3t.bkt.clouddn.com/banner.png
---

### 图片懒加载
懒加载是前端优化的一种技术，旨在用户进入页面后，当滚动页面将要到达图片位置时才加载图片。
加快页面加载速度，极大的提升了用户体验，也避免了用户进入页面之后就发送n多个图片请求，服务器吃不消啊！

### 实现原理
先将图片的```src```设置为空或者小的图片，将真实的图片地址存在```img```的自定义属性中，比如```data-src```中，等到页面滚动至图片位置时将真实图片位置复制给src属性。

1. 页面中的img元素，如果没有src属性，浏览器就不会发出请求去下载图片
2. 用户滚动页面至图片位置时，img元素获取到真正的路径后，开始发送请求加载图片

### JS中位置相关
> * ```screenLeft/screenX```: 窗口相对于屏幕左边的位置 
> * ```screenTop/screenY```: 窗口相对于屏幕上边的位置

**表示的是从屏幕左边和上边到window对象表示的可见区域的距离**。

```javascript
//FF中支持 screenX 和 screenY
let leftPos = (typeof window.screenLeft == 'Number') ? window.screenLeft : window.screenX;
let TopPos = (typeof window.screenTop == 'Number') ? window.screenTop : window.screenY;
```

若window对象是最外层对象，而且浏览器窗口贴紧屏幕上方，则 ```screenTop/screenY``` 为 0

> * ```clientWidth/clientHeight``` : 页面视口大小信息（ALL，注意获取方式）
> * ```innerWidth/innerHeight``` : 获取页面视口大小（页面尺寸）,页面视图容器大小
> * ```outerWidth/outerHeight``` : 获取浏览器窗口本身的大小（IE9+、Safari、FF）

```javascript
let pageWidth = window.innerWidth;
let pageHeight = window.innerHeight;

if( typeof pageWidth != 'Number'){
    if(document.compatMode == 'CSS!Compat'){
        //标准模式
        pageWidth = document.documentElement.clientWidth;
        pageHeight = document.documentElement.clientHeight;
    } else {
        //怪异模式（混杂模式）
        pageWidth = document.body.clientWidth;
        pageHeight = document.body.clientHeight;
    }
}
```

### 懒加载实现

```javascript
var imgCurrent = 4;//初始化页面加载图片个数
var imgCount = 40;//总图片数
var height = document.body.clientHeight || document.documentElement.clientHeight;
var scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
var clientHeight = Math.min(document.documentElement.scrollHeight, document.documentElement.clientHeight);
var img = document.getElementsByTagName('img');

window.onscroll = null;
window.onscroll = () => {
    //图片懒加载
    for (var i = imgCurrent; i < imgCount; i++) {
        if (img[i].offsetTop < clientHeight + scrollTop) {
            img[i].src = img[i].getAttribute('data-src');
            img[i].style.opacity = 1;
            imgCurrent = i + 1;
            console.log('图片加载[' + i + ']:' + img[i].src);
        }
    }
};
```

<!-- <script async src="//jsfiddle.net/wangyutao/wd70mk9q/16/embed/"></script> -->

### 补充

![位置](http://ow9cw9x3t.bkt.clouddn.com/js-position.jpg)

#### 偏移量(```offset```)
> * ```offsetWidht``` : 元素在水平方向上占用的空间大小。包括元素的宽度、水平滚动条的宽度、左右边框的宽度。
> * ```offsetHeight``` : 元素在垂直方向上占用的空间大小。包括元素的高度、垂直滚动条的高度、上下边框的高度。
> * ```offsetLeft``` : 元素的左边框至包含元素的左内边距的距离。（offsetParent） 
> * ```offsetTop``` : 元素的上边框至包含元素的上内边距的距离。（offsetParent）

```offsetParent```为相对于元素定位的父级元素
```offsetTop``` 和 ```offsetLeft``` 与其包含元素```offsetParent```有关。```offsetParent```的值不一定与```parentNode```相同。
这些偏移量属性均为**只读**。
![偏移量 offset](http://ow9cw9x3t.bkt.clouddn.com/offset.jpg)


#### 客户区大小（```client dismension```）

> * clientWidth : 元素内容区宽度加上左右内边距。```content + padding-left + padding-right```
> * clientHeight : 元素内容区高度加上上下内边距。```content + padding-top + padding-bottom```

client dismension 值也是**只读**的。

```javascript
let clientWidth = document.documentElement.clientWidht;
let clientHeight = document.documentElement.clientHeight;
```

#### 滚动大小（```scroll dismension```）

> * ```scrollTop``` : 被隐藏在内容区域上方的高度。（上方被隐藏了多少）
> * ```scrollLeft``` : 被隐藏在内容区域左侧的宽度。（左侧被隐藏了多少）
> * ```scrollWidth``` : 在没有滚动的情况下，元素内容的总宽度。
> * ```scrollHeight``` : 在没有滚动的情况下，元素内容的总高度。

* 带有垂直滚动条的页面总高度：```document.documentElement.scrollHeight```
* 带有水平滚动条的页面总宽度：```document.documentElement.scrollWidth```
* 通过scrollLeft和scrollTop既可以确定元素当前滚动的状态，也可以设置元素的滚动位置。

```javascript
// 确定文档的总高度
//scrollHeight和clientHeight中的最大值
let docHeight = Math.max(documnt.documentElement.scrollHeight, document.documntElement.clientHeight);

// 确定文档的总宽度
//scrollWidth和clientWidth中的最大值
let docWidth = Max.max(document.documentElement.scrollWidth, document.documentElement.clientWidth);
```