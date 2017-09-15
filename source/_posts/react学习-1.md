---
layout: react
title: react学习-1
date: 2017-09-15 17:43:17
tags:
thumbnail: http://ow9cw9x3t.bkt.clouddn.com/react.jpg
---

### JSX语法

JSX 既不是字符串也不是HTML，是JavaScript的语法扩展，将被解析成JavaScript的一个对象。JSX用于生成React的“元素”。
JSX中可以嵌入js表达式，用```｛｝```包裹。

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