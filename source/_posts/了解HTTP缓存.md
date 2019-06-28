---
title: 了解HTTP缓存
toc: true
categories: [Javascript]
date: 2018-04-09 15:53:46
tags: [Javascript, cache, 缓存]
thumbnail:
---

在前端开发中，缓存有利于加快网页的加载速度，也是一种提高前端网站性能的常用方法。同时缓存可以被反复利用，减少流量和带宽的开销。

重用已获取的资源能够有效的提升网站与应用的性能。Web 缓存能够减少延迟与网络阻塞，进而减少显示某个资源所用的时间。借助 HTTP 缓存，Web 站点变得更具有响应性。([MDN HTTP缓存](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Caching_FAQ))

<!-- more -->

当 web 缓存发现请求的资源已经被存储，它会拦截请求，返回该资源的拷贝，而不会去源服务器重新下载。这样带来的好处有：缓解服务器端压力，提升性能(获取资源的耗时更短了)。对于网站来说，缓存是达到高性能的重要组成部分。缓存需要合理配置，因为并不是所有资源都是永久不变的：重要的是对一个资源的缓存应截止到其下一次发生改变（即不能缓存过期的资源）。

缓存的种类：
* CDN缓存
* 数据库缓存（H5新增加的localstorage和数据库缓存，应用层缓存）
* 代理服务器缓存
* 浏览器缓存（主要是指http缓存，即协议层）

浏览器缓存可以分为 `强缓存` 和 `协商缓存`，可以在 `HTTP协议头` 和 `HTML页面的 meta 标签` 中定义 。缓存分别从 `新鲜度` 和 `校验值` 两个维度来规定浏览器是否可以直接使用缓存中的副本，还是直接去服务器获取最新版本。

* 新鲜度（过期机制）： 也就是缓存副本的有效期（过期时间或者有效时间）。
* 校验值（验证机制）： 资源第一次请求后服务器返回会在控制头信息带上这个资源的实体标签（ Etag / Last-Modified ），这个信息可以用来作为浏览器再次请求过程的校验标识。如果服务器校验不匹配，说明资源已经被修改或者过期，服务器将新的资源重新返回给客户端。

## 强缓存

强缓存：只有当缓存资源失效时，才会去服务器获取最新的资源。在 `HTTP header` 中，可以是设置强缓存的两个字段： `Expires` 和 `Cache-Control`。

强缓存表示在缓存期间不需要在请求， `status code` 直接返回 `200`。

强缓存过程：
1. 浏览器第一次跟服务器请求一个资源，服务器在返回这个资源的同时，在 `response` 的 `header` 会加上 `Expires/cach-control` ；
2. 浏览器再请求这个资源时，先从缓存中寻找，找到这个资源后，比较 `expires` 或 `cache-control的max-age` 字段值, 如果在有效期内，则缓存命中，读取缓存内容（`200 from cache`），否则重新向服务器发送请求；
3. `Header` 在重新加载的时候会被更新。

### Pragam

`HTTP/1.0` ,值为 `no-cache` 时强制禁用缓存。

### Expires

Expires 表示缓存的 `过期时间`，`HTTP/1.0`，是绝对时间（具体某一个时间点）。
```http
Expires: Thu, 09 Nov 2018 08:45:11 GMT
```

响应报文中 Expires 定义的缓存时间是相对服务器上的时间而言的，其定义的是资源 `失效时刻` 。**也就是说 `Expires` 的定义时间是根据服务器的时间定义的，但是客户端比较的时候是用本地时间比较**。如果客户端上的时间和服务器上的时间不一致，缓存没有意义。

### Cache-control

`Cache-Control` 指定了资源的 `最大有效时间` 或者缓存策略，`HTTP/1.1` 。在该时间内，客户端不需要向服务器发送请求。

`HTTP/1.1` 定义的 `Cache-Control` 头用来区分对缓存机制的支持情况， 请求头和响应头都支持这个属性。通过它提供的不同的值来定义缓存策略。

Cache-Control值类型

<table>
  <colgroup>
    <col width="150px">
    <col width="150px">
    <col width="">
  </colgroup>
  <thead>
    <tr>
      <th>值</th>
      <th>含义</th>
      <th>备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>no-cache</td>
      <td>强制确认缓存</td>
      <td>每次有请求发出时，缓存会将此请求发到服务器，服务器端会验证请求中所描述的缓存是否过期，若未过期（注：实际就是返回 <code>304</code>），则缓存才使用本地缓存副本。</td>
    </tr>
    <tr>
      <td>no-store</td>
      <td>禁止进行缓存</td>
      <td>缓存中不得存储任何关于客户端请求和服务端响应的内容。每次由客户端发起的请求都会下载完整的响应内容。</td>
    </tr>
    <tr>
      <td>max-age</td>
      <td>缓存过期时间</td>
      <td><code>max-age=&lt;seconds&gt;</code>，表示资源能够被缓存的最大时间。相对 <code>Expires</code> 而言，<code>max-age</code> 是距离请求发起的时间的秒数。针对应用中那些不会改变的文件，通常可以手动设置一定的时长以保证缓存有效，例如图片、css、js 等静态资源。</td>
    </tr>
    <tr>
      <td>public</td>
      <td>公共缓存</td>
      <td>表示该响应可以被任何中间人（比如中间代理、CDN 等）缓存。指定 public ，则一些通常不被中间人缓存的页面（如带有 HTTP 验证信息账号密码等 的页面或者某种特定状态的页面）也会被其缓存</td>
    </tr>
    <tr>
      <td>private（默认）</td>
      <td>私有缓存</td>
      <td>中间人不能缓存，该响应只能应用于浏览器私有缓存中。</td>
    </tr>
  </tbody>
</table>

## 协商缓存

* `Last-Modified / If-Modified-Since` 在约定有效期的基础上，增加文件服务器上的最后修改时间进行再次验证
* `Etag / If-None-Match` 在约定有效期的基础上，增加`文件版本号`的验证

### Last-Modified / If-Modified-Since

判断过程：
1. 浏览器第一次向服务器请求一个资源，服务器在返回这个资源的同时，在 `respone` 的 header 加上 `Last-Modified` 字段，表示该资源在服务器上的最后修改时间；
2. 浏览器再次向服务器请求这个资源时，在 `request` 的 header 上加上 `If-Modified-Since` 字段，这个值就是上一次请求时返回的 `Last-Modified` 的值;
3. 服务器收到资源请求时，比较 `If-Modified-Since` 和 `Last-Modified` 字段值，若相同，则说明文件没有修改，返回304 Not Modified, 浏览器从缓存中加载资源；若不相同，说明文件被更新，浏览器直接从服务器加载资源, 返回200；
4. 重新加载资源时更新 `Last-Modified` Header

```http
Last-Modified: Tue, 12 Jan 2016 03:08:53 GMT 
If-Modified-Since: Tue, 12 Jan 2016 03:08:53 GMT
```
缺点：
* `Last-Modified` 标注的最后修改只能精确到秒级，如果某些文件在1秒钟以内，被修改多次的话，它将不能准确标注文件的修改时间
* 如果某些文件会被定期生成，但有时内容并没有任何变化（仅仅改变了时间），但 `Last-Modified` 却改变了，导致文件没法使用缓存
* 有可能存在服务器没有准确获取文件修改时间，或者与代理服务器时间不一致等情形

### Etag / If-None-Match

`ETag` 解决了 `Last-Modifiend` 的缺陷，`ETag` 不仅仅跟最后修改时间决定, 它是根据当前请求的资源生成的一个唯一标识符（默认是由文件的索引节（INode），大小（Size）和最后修改时间（MTime）进行 Hash 后得到的)

判断过程：
1. 浏览器第一次向服务器请求一个资源，服务器在返回这个资源的同时，在 `respone` 的 header 加上 `ETag` 字段；
2. 浏览器再次跟服务器请求这个资源时，在 `request` 的 header 上加上 `If-None-Match` ，这个值就是上一次请求时返回的 `ETag` 的值；
3. 服务器再次收到资源请求时，再根据资源生成一个新的 `ETag` ，与浏览器传过来 `If-None-Match` 比较，如果这两个值相同就说明资源没有变化，则返回 `304 Not Modified` ，浏览器从缓存中加载资源，否则返回 `200` 并返回新的资源内容。

与 `Last-Modified` 不一样的是，当服务器返回 `304 Not Modified` 的响应时，由于 `ETag` 重新生成过，response header 中还会把这个 `ETag` 返回，即使这个 `ETag` 跟之前的没有变化。

`Etag` 主要为了解决 `Last-Modified` 无法解决的一些问题：

1. 一些文件也许会周期性的更改，但是他的内容并不改变(仅仅改变的修改时间)，这个时候我们并不希望客户端认为这个文件被修改了，而重新GET；
2. 某些文件修改非常频繁，比如在秒以下的时间内进行修改，(比方说1s内修改了N次)，If-Modified-Since能检查到的粒度是s级的，这种修改无法判断(或者说UNIX记录MTIME只能精确到秒)；
3. 某些服务器不能精确的得到文件的最后修改时间。

[http缓存机制浅析](http://juanha.coding.me/2017/03/05/http-cache/)
[HTTP缓存控制小结](https://imweb.io/topic/5795dcb6fb312541492eda8c)

## 缓存优先级

* 强缓存 > 协商缓存
* Pragam > Cache-Control > Expires > Etag > Last-Modified