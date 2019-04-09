---
title: SVG基础入门
date: 2017-09-27 11:37:17
tags: [css, SVG]
categories: [CSS]
toc: true
# thumbnail: http://cloud.xuww.wang/nianshaodeni.png
---

> 可缩放矢量图形，即SVG，是W3C XML的分枝语言之一，用于标记可缩放的矢量图形。（摘自MDN）

* `version`： 表示` <svg> `的版本
* `xmlns`：http://www.w3.org/2000/svg 固定值
* `xmlns:xlink`：http://www.w3.org/1999/xlink 固定值
* `xml:space`：preserve 固定值，上述三个值固定，表示命名空间，当数据单独存在svg文件内时，这3个值不能省略
* `class`: class类名
* `width | height`： 定义 `svg` 画布的大小
* `viewbox`： 定义了画布上可以显示的区域，当 `viewBox` 的大小和 `svg` `不同时，viewBox` 在屏幕上的显示会缩放至 `svg` 同等大小。

<!-- more -->
有了 `svg` 标签，我们就可以愉快的在内部添加 `SVG` 图形了。

```html
<?xml version="1.0" standalone="no"?>

<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="100%" height="100%" version="1.1" xmlns="http://www.w3.org/2000/svg">
    <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red"/>
</svg>
```
<svg width="100%" height="100%" version="1.1" xmlns="http://www.w3.org/2000/svg">
    <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red"/>
</svg>

> * 第一行包含了 XML 声明。standalone 属性规定此 SVG 文件是否是“独立的”，或含有对外部文件的引用。standalone="no" 意味着 SVG 文档会引用一个外部文件。
> * SVG 代码以 ```<svg> ```元素开始，包括开启标签 ```<svg>``` 和关闭标签```</svg>``` 。```width``` 和 ```height``` 属性可设置此 SVG 文档的宽度和高度。```version```属性可定义所使用的 ```SVG``` 版本，```xmlns``` 属性可定义 SVG 命名空间。

![SVG](http://cloud.xuww.wang/svg.jpg)
