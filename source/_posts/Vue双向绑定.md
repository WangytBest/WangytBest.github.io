---
title: Vue双向绑定
toc: true
tags: [Vue]
categories: [Vue]
date: 2019-04-09 16:03:43
thumbnail:
---

### 双向绑定

MVVM：数据变化更新试图，视图变化更新数据。
* Model
* View
* ViewModel

<!-- more -->

### 双向绑定实现
* vue: 数据劫持
vue数据实现双向绑定是通过数据劫持结合发布者-订阅者模式实现的。

* angular: 脏检查机制
当触发了指定事件后会进入脏数据检测，这时会调用 `$digest` 循环遍历所有的数据观察者，判断当前值是否和先前的值有区别，如果检测到变化的话，会调用 `$watch` 函数，然后再次调用 `$digest` 循环直到发现没有变化。循环至少为二次 ，至多为十次。

### vue实现

> vue.js 是采用`数据劫持`结合`发布/订阅模式`的方式，通过`Object.defineProperty()`来劫持各个属性的 `setter`  、 `getter` ，在数据变动时发布消息给订阅者，触发相应的监听回调。

1. 需要 `observe` 的数据对象进行递归遍历，包括子属性对象的属性，都加上 `setter` 和 `getter` 。这样的话，给这个对象的某个值赋值，就会触发 `setter` ，那么就能监听到了数据变化；
2. `compile` 解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图；
3. `Watcher订阅者` 是 `Observer` 和 `Compile` 之间通信的桥梁，主要做的事情是:
    1、在自身实例化时往 `属性订阅器(dep)` 里面添加自己
    2、自身必须有一个 `update()方法`
    3、待属性变动 `dep.notice()` 通知时，能调用自身的 update() 方法，并触发 Compile 中绑定的回调，则功成身退。
4. MVVM 作为数据绑定的入口，整合 `Observer` 、 `Compile` 和 `Watcher` 三者，通过 Observer 来监听自己的 model 数据变化，通过 Compile 来解析编译模板指令，最终利用Watcher 搭起 Observer 和 Compile 之间的通信桥梁，达到 `数据变化 -> 视图更新` 、`视图交互变化(input) -> 数据model变更` 的双向绑定效果。

实现数据的双向绑定，首先要对数据进行劫持监听，设置一个 `监听器Observer` ，用来监听所有属性。如果属性发上变化了，就需要告诉 `订阅者Watcher` 看是否需要更新。因为订阅者是有很多个，所以我们需要有一个 `消息订阅器Dep` 来专门收集这些订阅者，然后在 `监听器Observer` 和 `订阅者Watcher` 之间进行统一管理。接着，我们还需要有一个 `指令解析器Compile` ，对每个节点元素进行扫描和解析，将相关指令对应初始化成一个 `订阅者Watcher` ，并替换模板数据或者绑定相应的函数，此时当 `订阅者Watcher` 接收到相应属性的变化，就会执行对应的更新函数，从而更新视图。

![双向绑定(来源 https://segmentfault.com/a/1190000006599500 )](http://blog.cloud.xuww.wang/vue%E5%8F%8C%E5%90%91%E7%BB%91%E5%AE%9A.png)

#### 1. 监听器Observer
> 实现一个 `监听器Observer` ，用来劫持并监听所有属性，如果有变动，就通知 `订阅者Watcher` 。

```javascript
function defineReactive(data, key, value) {
    observe(val); // 递归遍历所有子属性
    var dep = new Dep();
    Object.defineProperty(data, key, {
        enumerable: true,
        configurable: true,
        set: function(newVal) {
            if( val === newVal ) {
                return;
            }
            value = newVal;
            dep.notify(); // 如果数据变化，通知所有订阅者
        },
        get: function() {
            if(Dep.target) { // 判断是否需要添加订阅者
                dep.addSub(Dep.target); // 添加订阅者
            }
            return value;
        }
    })
}

// 递归遍历所有子属性
function observe(data) {
    if(!data || typeof data !== 'object') {
        return;
    }
    Object.keys(data).forEach(key => {
        defineReactive(data, key, data[key]);
    })
}
```

我们将 `订阅器Dep` 添加一个订阅者设计在 `getter` 里面，这是为了让 Watcher 初始化进行触发，因此需要判断是否要添加订阅者。
在 `setter` 函数里面，如果数据变化，就会去通知所有 `订阅者Watcher`，订阅者们就会去执行对应的**更新的函数 update()**。

#### 2. 消息订阅器Dep

> 实现一个 `消息订阅器Dep` ，主要**负责收集订阅者**，然后在属性变化的时候执行对应 `订阅者Watcher` 的更新函数。

维护一个数组，用来收集订阅者，数据变动触发 notify ，再调用订阅者的 update方法。

```javascript
function Dep() {
    this.subs = [];
}

Dep.property.addSub = function(sub) {
    this.subs.push(sub);
}
Dep.property.notify = function() {
    this.subs.forEach(sub => {
        sub.update();
    })
}

Dep.target = null;
```

`监听器Observer` 是在 `get函数` 执行了添加 `订阅者Watcher` 的操作，所以在 `订阅者Watcher` 初始化的时候触发对应的 `get` 函数去执行添加订阅者操作。注意只在 `订阅者Watcher` 初始化的时候才需要添加订阅者。

#### 3. 订阅者Watcher

> 实现一个`订阅者Watcher`，可以收到属性的变化通知并执行相应的函数，从而更新视图。

```javascript
function Watcher(vm, exp, cb) {
    this.cb = cb;
    this.vm = vm;
    this.exp = exp;
    this.value = this.get();  // 将自己添加到订阅器的操作
}
 
Watcher.prototype = {
    update: function() {
        this.run();
    },
    run: function() {
        var value = this.vm.data[this.exp];
        var oldVal = this.value;
        if (value !== oldVal) {
            this.value = value;
            this.cb.call(this.vm, value, oldVal);
        }
    },
    get: function() {
        Dep.target = this;  // 缓存自己
        var value = this.vm.data[this.exp]  // 强制执行监听器里的get函数
        Dep.target = null;  // 释放自己
        return value;
    }
};
```

#### 关联 Wathcher 和 Observer 

到此为止，简单版的Watcher设计完毕，这时候我们只要将 Observer 和 Watcher 关联起来，就可以实现一个简单的双向绑定数据了。

```html
<body>
  <h1 id="name">{{name}}</h1>
</body>
```

```javascript
// Observer和Watcher关联起来
function SelfVue (data, el, exp) {
    this.data = data;
    observe(data); // 1. Observe
    el.innerHTML = this.data[exp];  // 初始化模板数据的值
    new Watcher(this, exp, function (value) { // 2. Watcher
        el.innerHTML = value;
    });
    return this;
}
```

```javascript
var ele = document.querySelector('#name');
var selfVue = new SelfVue({
    name: 'hello world'
}, ele, 'name');

window.setTimeout(function () {
    console.log('name值改变了');
    selfVue.data.name = 'canfoo';
}, 2000);
```

#### 4. 解析器Compile
实现一个`解析器Compile`，可以扫描和解析每个节点的相关指令，并根据初始化模板数据以及初始化相应的订阅器。

compile 主要做的事情是解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图。

#### 数据劫持

`Object.defineProperty()`方法实现数据劫持，`Object.defineProperty()`用来控制对象属性，比如读写权限、是否可枚举、描述属性`get`和`set`等。
