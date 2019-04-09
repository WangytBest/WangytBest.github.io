---
layout: react
title: React-JSX
date: 2017-09-15 17:43:17
tags: React
categories: [React]
thumbnail: http://cloud.xuww.wang/react.jpg
---

### JSX语法

> JSX 既不是字符串也不是HTML，是JavaScript的语法扩展，将被解析成JavaScript的一个对象。JSX用于生成React的“元素”。JSX中可以嵌入js表达式，用```｛｝```包裹。
<!-- more -->
```javascript
function formatName(user) {
    return user.firstName + ' ' + user.lastName; 
}

const user = {
    firstName: 'Harper',
    lastName: 'Perez'
}

const element = (
    <h1>Hello, {formatName(user)} !</h1>
)

ReactDOM.render(
    element,
    document.getElementById('root')
)
```

<iframe width="100%" height="300" src="//jsfiddle.net/wangyutao/z2pzn6xh/22/embedded/js,html,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>


### JSX指定属性
* 使用引号将字符串文字指定为属性值
```javascript
const element = <div tabIndex="0"></div>
```
* 使用花括号```{}```将JavaScript表达式嵌入属性中，｛｝中的变量不需要用""括起来，否则将解析为字符串
```javascript
const element = <img src={user.avtarurl} />
```

### JXS包含子标签

> JSX可以包含子标签

> * JSX最外层只能包含一个标签，父标签内可以嵌套任意的子标签
> * JSX 标签内的属性命名约定使用 ```camelCase```方式命名，而不是HTML属性名称

```javascript
const element = (
    <div className="demo">
        <h1>Hello!</h1>
        <h2>Good to see you!</h2>
    </div>
)

const elemtent = (
    <div tabIndex="0"></div>
)
```

### JSX转换

Bebel将JSX转换编译成```React.createElement()```对象。

```javascript
const element = (
    <h1 className="greeting">
        Hello, World!
    </h1>
)
```

```javascript
const element = React.createElement(
    'h1',
    {className: 'greeting'},
    'Hello, World!'
)
```

以上两种方式是等价的，最后都会转换成React Elements，这些对象组成页面的DOM并且保持更新。

解析为react Elements

```js   
const element = {
    type: 'h1',
    props: {
        className: 'greeting',
        children: 'Hello, World!'
    }
}
```

