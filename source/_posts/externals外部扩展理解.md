---
title: externals外部扩展理解
toc: true
tags: [webpack]
categories: [webpack]
date: 2019-04-09 16:00:44
thumbnail:
---

如果我们想引用一个库，但是又不想让webpack打包，并且又不影响我们在程序中以CMD、AMD或者window/global全局等方式进行使用，那就可以通过配置externals。

<!-- more -->
`externals` 配置选项提供从输出的`bundle`中排除依赖
>* 可以解决`npm run build`打包后`vender.js`文件过大的问题
>
>* 防止将某些`import`的包（package）打包到bundle（vue-cli2默认输出文件名为`vender.js`）中，而是运行时再从外部获取这些扩展依赖（external dependencies）,如第三方类库。

### 类型
> `string` `array` `object` `function` `regex`

### 配置

>配置externals，这样就剥离了那些不需要改动的依赖，不再把这些类库一起打包

```
// webpack.config.js
modules.exports = {
    ...
    externals: {
        'jquery': 'jQuery',
        'vue': 'Vue',
        'vue-router': 'VueRouter',
        'vuex': 'Vuex',
        lodash : {
            commonjs: 'lodash',
            amd: 'lodash',
            root: '_' // 指向全局变量
        }
    }
}
```

第二种方式描述了外部library所有可用的访问方式。这里`loadsh`这个外部的library可以在`AMD`和`CommonJS`模块系统中通过`loadsh`访问。但在`全局变量`形式下用`_`访问。

剥离第三方依赖，需要在`index.html`中引入
```html
    <script src="http://storage.jd.com/campus-inviting/vue.min.js"></script>
    <script src="http://storage.jd.com/campus-inviting/vue-router.min.js"></script>
    <script src="http://storage.jd.com/campus-inviting/vuex.min.js"></script>
```

[webpack externals 深入理解](https://segmentfault.com/a/1190000012113011)

