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

> *   


```javascript
let imgCurrent = 4;//初始化页面加载图片个数
let imgCount = 40;//总图片数
let height = Math.min(document.body.clientHeight, document.documentElement.clientHeight);
let img = document.getElementsByTagName('img');

window.onscroll = null;
window.onscroll = () => {

    let scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
    let clientHeight = document.body.clientHeight;
    let screenHeight = window.screenHeight;

    //图片懒加载
    for (let i = this.imgCurrent; i < this.imgCount; i++) {
        if (img[i].offsetParent.offsetTop < clientHeight + scrollTop) {
            img[i].src = img[i].getAttribute('data-src');
            img[i].style.opacity = 1;
            this.imgCurrent = i + 1;
            console.log('图片加载[' + i + ']:' + img[i].src);
        }
    }
};  
```



