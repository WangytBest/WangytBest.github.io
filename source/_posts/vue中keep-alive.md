---
title: vue中keep-alive
date: 2018-04-03 20:07:54
toc: true
categories: [Vue]
tags: Vue
---

## keep-alive使用
`<keep-alive>`包裹动态的组件，会缓存不活动的组件实例，而不是销毁他们。`<keep-alive>`是一个抽象的组件，他自身不会渲染一个DOM元素，也不会出现在父组件链中。
当组件在`<keep-alive>`组件内被切换，它的`actived`和`deactived`这两个生命周期钩子函数将会被对应执行。
> Vue2.2.0及以上版本，`activated` 和 `deactivated` 将会在 `<keep-alive>` 树内的所有嵌套组件中触发。
**主要用于保留组件状态或避免重新渲染。**

<!-- more -->

当引入`<keep-alive>`的时候，页面第一次进入，钩子的触发顺序`created` -> `mounted` -> `activated`，退出时触发`deactivated`。当再次进入（前进或者后退）时，只触发`activated`。

`<keep-alive>`之后页面模板第一次初始化解析变成HTML片段后，再次进入就不在重新解析而是读取内存中的数据，即，只有当数据变化时，才使用VirtualDOM进行diff更新。故，页面进入的数据获取应该在`activated`中也放一份。数据下载完毕手动操作DOM的部分也应该在`activated`中执行才会生效。

所以，应该`activated`中留一份数据获取的代码，或者不要`created`部分，直接将`created`中的代码转移到`activated`中。

```html
<!-- 基本 -->
<keep-alive>
  <component :is="view"></component>
</keep-alive>

<!-- 多个条件判断的子组件 -->
<keep-alive>
  <comp-a v-if="a > 1"></comp-a>
  <comp-b v-else></comp-b>
</keep-alive>

<!-- 和 `<transition>` 一起使用 -->
<transition>
  <keep-alive>
    <component :is="view"></component>
  </keep-alive>
</transition>
```

## include 和 exclude 

**include 和 exclude 属性允许组件有条件地缓存。**二者都可以用逗号分隔字符串、正则表达式或一个数组来表示：
```html
<!-- 逗号分隔字符串 -->
<keep-alive include="a,b">
  <component :is="view"></component>
</keep-alive>

<!-- 正则表达式 (使用 `v-bind`) -->
<keep-alive :include="/a|b/">
  <component :is="view"></component>
</keep-alive>

<!-- 数组 (使用 `v-bind`) -->
<keep-alive :include="['a', 'b']">
  <component :is="view"></component>
</keep-alive>
```

## actived 和 deactived
* 类型：`Function`
* 说明：`<keep-alive>`组件 **激活/停用** 时调用（该钩子在服务器端渲染期间不被调用）

## 应用

项目开发中，使用`Vue2.0` 搭配路由切换`vue-router`，所有路径匹配到的视图组件都会被缓存。
如何使某些组件不缓存？

```html
<keep-alive>
    <router-view>
        <!-- 所有路径匹配到的视图组件都会被缓存！ -->
    </router-view>
</keep-alive>
```

#1. 使用`include`和`exclude`
```html
<keep-alive include='a,b,c' exclude='d,e,f'>
    <router-view>
        <!-- 所有路径匹配到的视图组件都会被缓存！ -->
    </router-view>
</keep-alive>
```

#2. 使用router.meta属性
设置路由，通过meta属性判断组件是否需要缓存

```javascript
// routes 配置
export default [
  {
    path: '/',
    name: 'home',
    component: Home,
    meta: {
      keepAlive: true // 需要被缓存
    }
  }, {
    path: '/:id',
    name: 'edit',
    component: Edit,
    meta: {
      keepAlive: false // 不需要被缓存
    }
  }
]
```

```html
<keep-alive>
    <router-view v-if="$route.meta.keepAlive">
        <!-- 这里是会被缓存的视图组件，比如 Home！ -->
    </router-view>
</keep-alive>

<router-view v-if="!$route.meta.keepAlive">
    <!-- 这里是不被缓存的视图组件，比如 Edit！ -->
</router-view>
```

部分转载[vue-router 之 keep-alive](https://blog.csdn.net/zgrkaka/article/details/73480947?locationNum=1&fps=1)