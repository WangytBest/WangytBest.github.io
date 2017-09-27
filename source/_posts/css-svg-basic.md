---
title: SVG基础入门
date: 2017-09-27 11:37:17
tags: [css, SVG]
---

```html
<?xml version="1.0" standalone="no"?>

<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

    <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red"/>

</svg>
```

> * 第一行包含了 XML 声明。standalone 属性规定此 SVG 文件是否是“独立的”，或含有对外部文件的引用。standalone="no" 意味着 SVG 文档会引用一个外部文件。
> * SVG 代码以 ```<svg> ```元素开始，包括开启标签 ```<svg>``` 和关闭标签```</svg>``` 。```width``` 和 ```height``` 属性可设置此 SVG 文档的宽度和高度。```version```属性可定义所使用的 ```SVG``` 版本，```xmlns``` 属性可定义 SVG 命名空间。

![SVG](http://ow9cw9x3t.bkt.clouddn.com/svg.jpg)
