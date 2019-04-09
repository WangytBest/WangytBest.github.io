---
title: Loadsh库模块化引入
toc: true
tags: [webpack]
categories: [webpack]
date: 2019-04-09 16:02:53
thumbnail:
---

## loadsh提供模块按需加载
> loadsh本身提供模块化引入，可按需引入

```javascript
// 
import { debounce } from 'loadsh'
import { throttle } from 'loadsh'

// 按需引入
import { debounce } from 'loadsh/debounce'
import { throttle } from 'loadsh/throttle'
```
<!-- more -->
## webpack plugin 配置
> 通过`webpack`配置，按需加载所需要的模块

* `loadsh-webpack-plugin`
* `babel-plugin-loadsh`

结合使用，将全路径引用的`loadsh`自动转变为模块化按需引用

```javascript
// @/util/loadsh.js 统一引入需要的loadsh方法
import _ from 'loadsh'

export default {
    cloneDeep: _.cloneDeep,
    debounce: _.debounce,
    throttle: _.throttle,
    isEmpty: _.isEmpty
}

// 注入全局 main.js
import _ from '@/util/loadsh.js'
Vue.prototype.$_ = _

// 组件使用
this.$_.debounce()

```