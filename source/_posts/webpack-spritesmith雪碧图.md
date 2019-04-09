---
title: webpack-spritesmith雪碧图
toc: true
tags: [webpack]
categories: [webpack]
date: 2019-04-09 16:02:00
thumbnail:
---

项目开发设计师没有提供svg或者icon-font，只能使用图片，过多的小图片造成资源浪费，解决方案：webpack打包将多个图标合成雪碧图

**需要同时配置开发环境和线上环境的webpack配置**

* `webpack-spritesmith` 合成雪碧图插件
* `file-loader`

<!-- more -->
-----
    | build
    |      |
    |      |--utils.js
    |      |--webpack.base.config.js
    |      |--webpack.dev.config.js
    |      |--webpack.pro.config.js
    |
    |src
    |   |
    |   |--assets
    |   |        |
    |   |        |--css
    |   |        |--incons
    |   |
    |   |-sprites

### 1. 修改`webpack.base.config.js`

> * resolve
> * modules
>> 添加resolve和处理雪碧图资源的loader

```javascript
resolve: {
    modules: [
        'node_modules',
        'src/sprites' // 合成sprite图片地址
    ]
}

modules: {
    rules: [
        ...
        // 对需要合成雪碧图的资源不进行base64转换
        {
            test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
            exclude: path.join(__dirname, 'src/assets/icons'),
            loader: 'url-loader',
            options: {
                limit: 10000,
                name: utils.assetsPath('img/[name].[hash:7].[ext]')
            }
        },
        // 对图标单独设置，以便生成雪碧图
        {
            test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
            include: path.join(__dirname, 'src/assets/icons'),
            loaders: [
                'file-loader?name=i/[hash].[ext]' // 使用file-loader 对 png 图标进行设置
            ]
        },
    ]
}
```

### 2. 修改`webpack.dev.config.js`

> 添加plugin

```javascript
const utils = require('./utils')
const SpritesmithPlugin = require('webpack-spritesmith')

plugins: [
    // 雪碧图设置
    new SpritesmithPlugin({
      src: {
        cwd: path.resolve(__dirname, '../src/assets/icons'), // 图标根路径
        glob: '*.png' // 匹配任意 png 图标
      },
      target: {
        image: path.resolve(__dirname, '../src/sprites/sprites.png'), // 生成雪碧图目标路径与名称
        // 设置生成CSS背景及其定位的文件或方式
        css: [
          [
            path.resolve(__dirname, '../src/sprites/sprites.css'),
            { format: 'function_based_template' }
          ],
          [
            path.resolve(__dirname, '../src/sprites/_sprites.scss'),
            { format: 'handlebars_based_template' }
          ],
        ]
      },
      customTemplates: {
        'function_based_template': utils.cssTemplateFunction,
        'handlebars_based_template': utils.scssTemplateFunction
      },
      apiOptions: {
        cssImageRef: "~sprites.png", // css文件中引用雪碧图的相对位置路径配置
      },
      // retina: '@2x',
      spritesmithOptions: {
        padding: 8,
      },
      // When set to true will console.log list of created files.
      logCreatedFiles: true
    }),
]
```

### 3.修改`utils.js`

> 打包中使用`webpack-spritesmith`插件使用自定义生成css/scss文件的模版方法

```javascript
exports.cssTemplateFunction = data => {
  const shared = '.icon { background-image: url(I); }'
      .replace('I', data.sprites[0].image);
  // 注意：此处默认图标使用的是二倍图
  const perSprite = data.sprites.map(function (sprite) {
    // background-size: SWpx SHpx;
    return '.icon-N { width: Wpx; height: Hpx; background-position: Xpx Ypx;}'
    // return '.icon-N { width: SWpx; height: SHpx; background-position: Xpx Ypx;}\n.icon-N .icon, .icon-N.icon { width: Wpx; height: Hpx; background-position: Xpx Ypx; } '
      .replace(/N/g, sprite.name)
      .replace(/SW/g, sprite.width / 2)
      .replace(/SH/g, sprite.height / 2)
      .replace(/W/g, sprite.width)
      .replace(/H/g, sprite.height)
      .replace(/X/g, sprite.offset_x)
      .replace(/Y/g, sprite.offset_y);
  }).join('\n');

  return shared + '\n' + perSprite;
};

exports.scssTemplateFunction = data => {
  // console.log(data, '==========', data.spritesheet)
  const mixs = `$screen:750;
                @function px2rem($px) {
                  @return #{$px/($screen/10)}rem
                }`
  const shared = '.icon { background-image: url(I); background-size: px2rem\(W\) px2rem\(H\);}'
      .replace('I', data.sprites[0].image)
      .replace(/W/g, data.spritesheet.width)
      .replace(/H/g, data.spritesheet.height)
  // 注意：此处默认图标使用的是二倍图
  const perSprite = data.sprites.map(function (sprite) {
    return '.icon-N { width: px2rem\(W\); height: px2rem\(H\); background-position: px2rem\(X\) px2rem\(Y\);} '
      .replace(/N/g, sprite.name)
      .replace(/SW/g, sprite.width / 2)
      .replace(/SH/g, sprite.height / 2)
      .replace(/W/g, sprite.width)
      .replace(/H/g, sprite.height)
      .replace(/X/g, sprite.offset_x)
      .replace(/Y/g, sprite.offset_y);
  }).join('\n');

  return mixs + '\n' + shared + '\n' + perSprite;
};

```

> 参考
> * [雪碧图处理工具](https://github.com/HaoyCn/postcss-sprite-property)
> * [webpack-spritesmith github](https://github.com/mixtur/webpack-spritesmith)





