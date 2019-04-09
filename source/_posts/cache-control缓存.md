---
title: cache-control缓存
toc: true
categories: [Javascript]
date: 2019-04-09 15:53:46
tags:
thumbnail:
---

`Cache-Control`指定了请求和响应遵循的缓存机制。好的缓存机制可以减少对网络带宽的占用，可以提高访问速度，提高用户的体验，还可以减轻服务器的负担。

<!-- more -->
### Cache-Control值类型

#### (1) 请求Request：
* `no-cache` 不要读取缓存中的文件，要求向WEB服务器重新请求
* `no-store` 请求和响应都禁止被缓存
* `max-age` 表示当访问此网页后的`max-age`秒内再次访问不会去服务器请求，其功能与`Expires`类似，只是`Expires`是根据某个特定日期值做比较。一但缓存者自身的时间不准确.则结果可能就是错误的，而`max-age`显然无此问题。
  > Max-age的优先级也是高于Expires的。
* `max-stale` 允许读取过期时间必须小于`max-stale`值的缓存对象。
* `min-fresh` 接受其`max-age`生命期大于其当前时间跟`min-fresh`值之和的缓存对象`only-if-cached`告知缓存者,我希望内容来自缓存，我并不关心被缓存响应,是否是新鲜的.
* `no-transform` 告知代理,不要更改媒体类型,比如jpg,被你改成png.

#### (2) 响应Response：
* `public` 数据内容皆被储存起来，就连有密码保护的网页也储存，安全性很低
* `private` 数据内容只能被储存到私有的cache，仅对某个用户有效，不能共享
* `no-cache` 可以缓存，但是只有在跟WEB服务器验证了其有效后，才能返回给客户端
* `no-store` 请求和响应都禁止被缓存
* `max-age` 本响应包含的对象的过期时间
* `Must-revalidate` 如果缓存过期了，会再次和原来的服务器确定是否为最新数据，而不是和中间的proxy
* `max-stale` 允许读取过期时间必须小于max-stale 值的缓存对象。
* `proxy-revalidate`与Must-revalidate类似，区别在于：proxy-revalidate要排除掉用户代理的缓存的。即其规则并不应用于用户代理的本地缓存上。
-maxage 与max-age的唯一区别是,s-maxage仅仅应用于共享缓存.而不应用于用户代理的本地缓存等针对单用户的缓存. 另外,s-maxage的优先级要高于max-age.
* `no-transform` 告知代理,不要更改媒体类型,比如jpg,被你改成png.