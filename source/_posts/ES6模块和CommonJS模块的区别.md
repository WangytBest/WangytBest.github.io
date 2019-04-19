---
title: ES6模块和CommonJS模块的区别
toc: true
tags: [Javascript]
categories: [Javascript]
keywords: [Javascript, ES6模块和CommonJS模块的区别]
date: 2019-04-12 18:19:37
thumbnail:
---

ES6 模块与 CommonJS 模块的差异

<!-- more -->
## CommonJS

基本语法
1. 暴露模块：`module.exports = value`或`exports.xxx = value`
2. 引入模块：`require(xxx)`,如果是第三方模块，xxx为模块名；如果是自定义模块，xxx为模块文件路径

```js
// example.js
var x = 5;
var addX = function (value) {
  return value + x;
};
module.exports.x = x;
module.exports.addX = addX;

// mian.js
var example = require('./example.js'); //如果参数字符串以“./”开头，则表示加载的是一个位于相对路径
console.log(example.x); // 5
console.log(example.addX(1)); // 6
```
## ES6

`ES6` 模块的设计思想是尽量的**静态化**，*使得编译时就能确定模块的依赖关系，以及输入和输出的变量*。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。比如，CommonJS 模块就是对象，输入时必须查找对象属性。

```js
/** 定义模块 math.js **/
var basicNum = 0;
var add = function (a, b) {
    return a + b;
};
export { basicNum, add };

/** 引用模块 **/
import { basicNum, add } from './math';
function test(ele) {
    ele.textContent = add(99 + basicNum);
}
```

## 区别

它们有两个重大差异：

① `CommonJS` 模块输出的是一个值的拷贝， `ES6` 模块输出的是值的引用。

② `CommonJS` 模块是运行时加载，ES6 模块是编译时输出接口。

第二个差异是因为 `CommonJS` 加载的是一个对象（即 `module.export`s 属性），该对象只有在脚本运行完才会生成。而 `ES6` 模块不是对象，它的对外接口只是一种静态定义，在代码静态解析阶段就会生成。

下面重点解释第一个差异，我们还是举上面那个CommonJS模块的加载机制例子:

```js
// lib.js
export let counter = 3;
export function incCounter() {
  counter++;
}
// main.js
import { counter, incCounter } from './lib';
console.log(counter); // 3
incCounter();
console.log(counter); // 4
```

`ES6` 模块的运行机制与 `CommonJS` 不一样。 `ES6` 模块是动态引用，并且不会缓存值，模块里面的变量绑定其所在的模块。

[前端模块化详解](https://github.com/ljianshu/Blog/issues/48)