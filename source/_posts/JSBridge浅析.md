---
title: JSBridge浅析
toc: true
tags: [Javascript, JSBridge]
categories: [Javascript]
keywords: [Javascript, JSBridge]
date: 2019-04-018 17:43:01
thumbnail:
---

### JSBridge 浅析

JSBridge 简单来讲，主要是给 Javascript 提供调用 Native 功能的接口，让 Hybrid 开发的前端人员可以方便的使用 Native 的地理位置、摄像头等原生功能。

实际上， JSBridge 就像是 Native 和 H5 之间的桥梁，构建 Native 和 非Native 间的双向消息通信的通道。

* JS 向 Native 发送消息：调用相关接口、通知 Native 当前 JS 状态等。
* Native 向 JS 发送消息： 回溯调用结果、消息推送、通知 JS 当前 Native 的状态等。

解决方案
* 基于 Web 的 Hybrid 的解决方案：微信浏览器、各大公司的 Hybrid 方案。
* ReactNative等。

<!-- more -->
### JSBridge 原理

JS 是运行在一个单独的 JS Context 中。Hybrid 方案是基于 WebView 的，JS 执行在 WebView 的 Webkit 引擎中。

Javascript 调用 Native 的方式主要有两种： 1. 注入API， 2. 拦截 URL SCHEME。

#### 注入 API

注入API 的主要原理是通过 WebView 提供的接口，向 Javascript 的 `window对象` 中注入对象或者方法，让 Javascript 调用时，直接执行相应的 Native 的代码逻辑。

* iOS 的 UIWebView
```js
window.postBridgeMessage(message);
```

* iOS 的 WKWebView
```js
window.webkit.messHandlers.naviteBridge.postMessage(message);
```

* Android
```js
window.nativeBridge.postMessage(message);
```

#### 拦截 URL SCHEME

URL SHEME: 为了方便 APP 直接相互调用，形式和普通的 URL 相似， protocol 和 host

主要流程：一般是通过修改iframe的src来实现，Web 端通过某种方式发送 URL SCHEME 请求，之后 Native 拦截到并根据 URL SCHEME 进行操作。

缺点
1. 使用 iframe.src 发送 URL SCHEME 会有 URL 长度的限制
2. 创建请求耗时

### JSBridge 接口实现

JSBridge 接口主要实现两个功能： 调用 Native 和 接收 Native 调用。

```js 
(function () {
  var id = 0,
    callbacks = {},
    registerFuncs = {};

    window.JSBridge = {
      // 调用 Native
      invoke: function(bridgeName, callback, data) {
        // 判断环境，获取不同的 nativeBridge
        var thisId = id ++; // 获取唯一 id
        callbacks[thisId] = callback; // 存储 Callback
        nativeBridge.postMessage({
          bridgeName: bridgeName,
          data: data || {},
          callbackId: thisId // 传到 Native 端
        });
      },
      receiveMessage: function(msg) {
        var bridgeName = msg.bridgeName,
            data = msg.data || {},
            callbackId = msg.callbackId, // Native 将 callbackId 原封不动传回
            responstId = msg.responstId;
        // 具体逻辑
        // bridgeName 和 callbackId 不会同时存在
        if (callbackId) {
          if (callbacks[callbackId]) { // 找到相应句柄
            callbacks[callbackId](msg.data); // 执行调用
          }
        } elseif (bridgeName) {
          if (registerFuncs[bridgeName]) { // 通过 bridgeName 找到句柄
            var ret = {},
                flag = false;
            registerFuncs[bridgeName].forEach(function(callback) => {
              callback(data, function(r) {
                flag = true;
                ret = Object.assign(ret, r);
              });
            });
            if (flag) {
              nativeBridge.postMessage({ // 回调 Native
                responstId: responstId,
                ret: ret
              });
            }
          }
        }
      },
      register: function(bridgeName, callback) {
        if (!registerFuncs[bridgeName])  {
          registerFuncs[bridgeName] = [];
        }
        registerFuncs[bridgeName].push(callback); // 存储回调
      }
    };
})();

```

[移动混合开发中的 JSBridge](https://blog.ymfe.org/%E6%B7%B7%E5%90%88%E5%BC%80%E5%8F%91%E4%B8%AD%E7%9A%84JSBridge/)