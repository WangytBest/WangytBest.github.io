---
title: ES6之Promise
toc: true
tags: [Javascript, ES6, Promise]
categories: [Javascript]
keywords: [Javascript, ES6, Promise]
date: 2019-05-08 17:25:09
thumbnail:
---

## Promise 对象

Promise 对象用于表示一个异步操作的最终状态（完成或失败），以及该异步操作的结果值。 [Promise - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)

<!-- more -->

`promise` 内部执行一些异步操作，一旦异步操作执行完毕，要么调用 `resolve` 函数来将 promise 状态改成 `fulfilled` ， 要么调用 `reject` 函数将 promise 状态改成 `rejected` 。 

```js
new Promise(function(resolve, reject) { ... } /* executor * /)
```

`Promise` 具有三个状态，初始状态为 `pending` ，异步操作成功状态转换为 `fulfilled` ， 失败转换为 `rejected` ，操作不可逆。当其中任何一种情况出现时， `Promise` 对象的 `then` 方法绑定的处理方法就会被调用（ `then` 方法包含两个参数： `onfuifilled` 和 `onrejected` 方法。当 `Promise` 状态为 `fulfilled` 状态时调用 `then` 的 `onFulfilled` 方法，当 `Promise` 状态为 `rejected` 时，调用 `then` 方法的 `onrejected` 方法.）

![Promise 状态修改](https://mdn.mozillademos.org/files/8633/promises.png)

* Promise.prototype.then(onFulfilled, onRejected)
* Promise.prototype.catch(onRejected)
* Promise.prototype.finally(onFinally)

* Promise.all(iterable)
* Promise.race(iterable)
* Promise.reject(reason)
* Promise.resolve(value)

### Promise.all(iterable)

`Promise.all` 方法用于将多个 Promise 实例包装成一个新的 Promise 实例。

```js
const p = new Promise.all([p1, p2, p3, ...]);
```

`p` 的状态有 `p1 p2 p3 ...` 决定，当所有的状态都变成 `fulfilled` ， `p` 的状态才会变成 `fulfilled` 状态，返回值是 `p1 p2 p3 ...` 的返回值组成的数组，传递给 `p` 的回调函数 `then` 。只要 `p1 p2 p3 ...` 中有一个被 `rejected` ， `p` 的状态就会变成 `rejected` ，此时第一个被 `rejected` 的实例的返回值会传递给 `p` 的回调 `catch` 。(**所有都成功则返回成功的数组，只要有一个失败则返回失败**)

> 如果失败的实例定义了自己的 `catch` 方法，那么它一旦被 `rejected` ，并不会触发 `Promise.all` 的 `catch` 方法

因为失败的 `Promise 实例（假设 p2 ）` 有自己的 `catch` 方法，该 `catch` 方法执行完成之后返回一个 `新的 Promise 实例` ，这个新的实例赋值给 `p2` ，则 `p2` 也会变成 `resolved` 状态，则 `Promise.all` 方法参数里面的所有实例都是 `resolved` 状态，因此还是会调用 `then` 方法。

```js
const p1 = new Promise((resolve, reject) => {
  resolve('hello');
})
.then(result => result)
.catch(e => e);

const p2 = new Promise((resolve, reject) => {
  throw new Error('报错了');
})
.then(result => result)
.catch(e => e);

Promise.all([p1, p2])
.then(result => console.log(result))
.catch(e => console.log(e));
// ["hello", Error: 报错了]
```

如果 `p2` 没有自己的 `catch` 方法，就会调用 `Promise.all()` 的 `catch` 方法。

```js
const p1 = new Promise((resolve, reject) => {
  resolve('hello');
})
.then(result => result);

const p2 = new Promise((resolve, reject) => {
  throw new Error('报错了');
})
.then(result => result);

Promise.all([p1, p2])
.then(result => console.log(result))
.catch(e => console.log(e));
// Error: 报错了
```

### Promise.race(iterable)

`Promise.race` 方法用于将多个 Promise 实例包装成一个新的 Promise 实例。

```js
const p = new Promise.race([p1, p2, p3, ...]);
```

只要 `p1 p2 p3 ...` 中有一个实例率先改变状态，则 p 的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给p的回调函数。

```js
// 面试题：给 ajax 请求设置 timeout
const p = Promise.race([
  fetch('/resource-that-may-take-a-while'),
  new Promise(function (resolve, reject) {
    setTimeout(() => reject(new Error('request timeout')), 5000)
  })
]);

p
.then(console.log)
.catch(console.error);
```

### Promise.finally(onFinally)

```js
/**
* Promise.prototype.finally
*/
Promise.prototype.finally = function(onFinally) {
  let P = this.constructor;
  return this.then(value => {
    P.resolve(onFinally()).then(() => value);
  }, reason => {
    P.resolve(onFinally()).then(() => { throw reason });
  })
}
```

[阮一峰 ES6](http://es6.ruanyifeng.com/#docs/promise#Promise-try)