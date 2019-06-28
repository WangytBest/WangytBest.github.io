---
title: JS控制GIF动画
date: 2018-02-02 10:14:25
categories: [Javascript]
tags:
---

> JS控制Gif动画

思想： 使用canvas获取Gif第一帧图片，静止的时候使用图片，播放的时候使用Gif。
<!-- more -->
```javascript
if ('getContext' in document.createElement('canvas')) {
    HTMLImageElement.prototype.play = function() {
        if (this.storeCanvas) {
            // 移除存储的canvas
            this.storeCanvas.parentElement.removeChild(this.storeCanvas);
            this.storeCanvas = null;
            // 透明度还原c
            this.style.opacity = '';
        }
        if (this.storeUrl) {
            this.src = this.storeUrl;
        }
    };
    HTMLImageElement.prototype.stop = function() {
        // polyfill 提供了这个方法用来获取设备的 pixel ratio
        let getPixelRatio = function(context) {
            let backingStore = context.backingStorePixelRatio ||
                context.webkitBackingStorePixelRatio ||
                context.mozBackingStorePixelRatio ||
                context.msBackingStorePixelRatio ||
                context.oBackingStorePixelRatio ||
                context.backingStorePixelRatio || 1;

            return (window.devicePixelRatio || 1) / backingStore;
        };
        let canvas = document.createElement('canvas');
        let ratio = getPixelRatio(canvas);
        // 尺寸
        let width = +this.width;
        let height = +this.height;
        if (width && height) {
            // 存储之前的地址
            if (!this.storeUrl) {
                this.storeUrl = this.src;
            }
            // canvas大小
            canvas.width = width * ratio;
            canvas.height = height * ratio;
            // 绘制图片帧（第一帧）
            // 注意，这里的 width 和 height 变成了 width * ratio 和 height * ratio
            canvas.getContext('2d').drawImage(this, 0, 0, width * ratio, height * ratio);
            canvas.style.width = width;
            canvas.style.height = height;
            // 重置当前图片
            try {
                this.src = canvas.toDataURL('image/gif');
            } catch (e) {
                console.log(e);
                // 跨域
                this.removeAttribute('src');
                // 载入canvas元素
                canvas.style.position = 'absolute';
                // 前面插入图片
                this.parentElement.insertBefore(canvas, this);
                // 隐藏原图
                this.style.opacity = '0';
                // 存储canvas
                this.storeCanvas = canvas;
            }
        }
    };
}
```