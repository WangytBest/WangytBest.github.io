---
title: webpack插件关于autoprefixer的冲突
date: 2018-08-27 11:15:54
toc: true
categories: [webpack]
tags: webpack
---

### 1. 实际遇到的问题
项目中经常会遇到css的一些奇怪问题，有些css属性的设置在在本地编译运行的时候是好的，但是打包上线之后这个属性就平白无故的没有了？

具体场景
在处理多行文本溢出时，需要使用`-webkit-box-orient: vertial`，在本地开发测试一切正常，但是在webpack编译之后，检查样式并没有这个属性，其他的属性都有。

<!-- more -->

```scss
// 多行文本
@mixin textmultiline($line:2) {
  display: -webkit-box;
  /* autoprefixer: off*/
  -webkit-box-orient: vertical;
  /* autoprefixer: on*/
  -webkit-line-clamp: $line;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

### 2. 为什么啊？
1. [why remove -webkit-box-orient property? #357](https://github.com/cssnano/cssnano/issues/357)

2. [Autoprefixer setting should be false by default #252](https://github.com/cssnano/cssnano/issues/252)

原因：
  autoprefixer自动的删除了一些它觉得没有必要的属性，所以解决办法就是设autoprefixer为false，或者针对某个属性忽autoprefixer


### 3. 怎么办

1. 属性忽略`autoprefixer`
```css
// eslint-disable-next-line
/* autoprefixer: off*/
-webkit-box-orient: vertical;
/* autoprefixer: on*/
```

2. 关闭`cssnano`的`autoprefixer`

> just remove the postcss config in vue-loader's config

Add the following option to prevent autoprefixer from removing prefixes (<strong>for cssnano v3 only</strong>):

```shell
{
  autoprefixer: {
    remove: false
  }
}
```
Then -webkit-box-orient will be preserved.

3. `optimize-css-assets-webpack-plugin` 插件问题

```cs
new OptimizeCSSPlugin({
  cssProcessorOptions: config.build.productionSourceMap
    ? { safe: true, map: { inline: false } }
    : { safe: true }
}),
```