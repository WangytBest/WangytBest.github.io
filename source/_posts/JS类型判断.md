---
title: JS类型判断
date: 2018-04-12 15:51:26
tags: [Javascript]
categories: [Javascript]
---

JS类型判断
<!-- more -->

## typeof

> typeof方法返回一个字符串，来表示数据的类型。

`typeof` 对于原始类型，除了 `null` 可以正确判断原始类型，(历史原因 null 以 0开头，跟 object 一样），对于对象来说，除了函数都会显示 `object` ，函数会显示 `function` 。

数据类型|type
-|:-:
Undefined|undefined
Null|object
布尔值|boolean
数值|number
字符串|string
Symbol|symbol
函数对象|function
任何其他对象|object
宿主对象(JS环境提供的，比如浏览器)|Implementation-dependent
---

```js
typeof 1 // 'number'
typeof NaN // 'number'
typeof '1' // 'string'
typeof undefined // 'undefined'
typeof true // 'boolean'
typeof Symbol() // 'symbol'
```

```javascript
var a = [];
var b = {};

typeof a; // "object"
typeof b; // "object"
typeof console.log // 'function'

a instanceof Object // true
b instanceof Object // true

a instanceof Array // true
b instanceof Array // false
```

## instanceof

如果想判断一个**对象**的正确类型，可以使用 `instanceof` ， `instanceof`内部机制是通过原型链来判断。

对于**原始类型**，不能直接通过 `instanceof` 来判断类型。

```js
function myInstanceof(left, right) {
  let prototype = right.prototype;
  left = left.__proto__;
  while(true) {
    if(left == null || left == undefined)
      return false;
    if(left == prototype)
      return true;
    left = left.__proto__;
  }
}
```

## 判断数组类型

### 支付宝base.js
```javascript
if ( value instanceof Array || 
  (!(value instanceof Object) && 
  (Object.prototype.toString.call((value)) == '[object Array]') || 
  typeof value.length == 'number' && 
  typeof value.splice != 'undefined' && 
  typeof value.propertyIsEnumerable != 'undefined' && 
  !value.propertyIsEnumerable('splice'))) { 
    return 'array'; 
} 
```
### instanceof
```javascript
var arr = []; 
arr instanceof Array; // true 
arr.constructor == Array; //true 
```

### call/apply
```javascript
Object.prototype.toString.call(value) == '[object Array]'

var isArray = function(obj) { 
  return Object.prototype.toString.call(obj) === '[object Array]'; 
} 
```

### ES6
```js
Array.isArray(obj);
```