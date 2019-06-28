---
title: 'vue项目中 -webkit-box-orient: vertical 打包后丢失解决办法'
toc: true
tags: []
categories: []
keywords: []
date: 2019-06-17 15:36:07
thumbnail:
---

第一种解决方法：

在 `package.json`文件中进行如下修改：

```js
"browserslist": [
  "> 1%",
  "last 2 versions",
  "not ie <= 8",
  "iOS >= 6",
  "Android > 4.1",
  "Firefox > 20"
]
```
 

第二种解决方法：

注释掉 `webpack.prod.conf.js` 中下面的代码

```js
new OptimizeCSSPlugin({
cssProcessorOptions: config.build.productionSourceMap
  ? { safe: true, map: { inline: false } }
  : { safe: true }
  }),
```
这段代码实现了 `css` 的压缩 注释掉就 `css` 就没有压缩了，所以 还要在 `utils.js` 中添加 `minimize:true`
```js
const cssLoader = {
  loader: 'css-loader',
    options: {
    sourceMap: options.sourceMap,
    minimize:true
  }
}
```
