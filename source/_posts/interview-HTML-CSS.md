---
title: 前端面试集（HTML+CSS）
date: 2017-09-15 16:46:10
tags: [HTML, CSS, 面试]
categories: [面试, 前端]
comments: true
thumbnail: http://cloud.xuww.wang/resume.gif
---

### 1. 浏览器页面有哪三层构成，分别是什么，作用是什么?

* 构成：结构层、表示层、行为层
* 分别是：HTML、CSS、JavaScript
* 作用：HTML实现页面结构，CSS完成页面的表现与风格，JavaScript实现一些客户端的功能与业务。

<!-- more -->
#### 2.HTML5的优点与缺点？

**优点：**
1. 网络标准统一、HTML5本身是由W3C推荐出来的。
2. 多设备、跨平台
3. 即时更新。
4. 提高可用性和改进用户的友好体验；
5. 有几个新的标签，这将有助于开发人员定义重要的内容；
6. 可以给站点带来更多的多媒体元素(视频和音频)；
7. 可以很好的替代Flash和Silverlight；
8. 涉及到网站的抓取和索引的时候，对于SEO很友好；
9. 被大量应用于移动应用程序和游戏。

**缺点：**
1. 安全：像之前Firefox4的web socket和透明代理的实现存在严重的安全问题，同时web storage、web socket 这样的功能很容易被黑客利用，来盗取用户的信息和资料。
2. 完善性：许多特性各浏览器的支持程度也不一样。
3. 技术门槛：HTML5简化开发者工作的同时代表了有许多新的属性和API需要开发者学习，像web worker、web socket、web storage 等新特性，后台甚至浏览器原理的知识，机遇的同时也是巨大的挑战
4. 性能：某些平台上的引擎问题导致HTML5性能低下。
5. 浏览器兼容性：最大缺点，IE9以下浏览器几乎全军覆没。

#### 3.Doctype作用? 严格模式与混杂模式如何区分？它们有何意义?
**作用**
1. 声明位于文档中的最前面，处于标签之前。告知浏览器的解析器，用什么文档类型 规范来解析这个文档。
2. 严格模式的排版和JS 运作模式是以该浏览器支持的最高标准运行。
3. 在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。
4. `DOCTYPE`不存在或格式不正确会导致文档以混杂模式呈现。

**意义** 
> `doctype`声明指出阅读程序应该用什么规则集来解释文档中的标记。在Web文档的情况下，“阅读程序”通常是浏览器或者校验器这样的一个程序，“规则”则是W3C所发布的一个文档类型定义（DTD）中包含的规则。

1. 声明位于文档中的最前面的位置，处于标签之前。此标签可告知浏览器文档使用哪种 HTML 或 XHTML 规范。该标签可声明三种 DTD 类型，分别表示严格版本、过渡版本以及基于框架的HTML 文档。
2. 所谓的标准模式是指，浏览器按 W3C 标准解析执行代码；怪异模式则是使用浏览器自己的方式解析执行代码，因为不同浏览器解析执行的方式不一样，所以我们称之为怪异模式。 严格模式是浏览器根据web标准去解析页面，是一种要求严格的DTD，不允许使用任何表现层的语法，如
。严格模式的排版和JS 运作模式是以该浏览器支持的最高标准运行混杂模式则是一种向后兼容的解析方法，说的透明点就是可以实现IE5.5以下版本浏览器的渲染模式。
3. 浏览器解析时到底使用标准模式还是怪异模式，与你网页中的 DTD 声明直接相关， DTD 声明定义了标准文档的类型（标准模式解析）文档类型，会使浏览器使用相应的方式加载网页并显示，忽略 DTD 声明 ,将使网页进入怪异模式。

### 4.HTML5有哪些新特性、移除了哪些元素？
> `Html5` **新增了 `27 `个元素，废弃了`16`个元素**，根据现有的标准规范，把 `HTML5` 的元素按优先级定义为结构性属性、级块性元素、行内语义性元素和交互性元素 4 大类。
1. **结构性元素主要负责web上下文结构的定义**
* `section`：在 web 页面应用中，该元素也可以用于区域的章节描述。
* `header`：页面主体上的头部， header 元素往往在一对 body 元素中。
* `footer`：页面的底部（页脚），通常会标出网站的相关信息。
* `nav`：专门用于菜单导航、链接导航的元素，是 navigator 的缩写。
* `article`：用于表现一篇文章的主体内容，一般为文字集中显示的区域。
2. **级块性元素主要完成web页面区域的划分，确保内容的有效分割**
* `aside`：用于表达注记、贴士、侧栏、摘要、插入的引用等作为补充主体的内容。
* `figure`：是对多个元素进行组合并展示的元素，通常与 ficaption 联合使用。
* `code`：表示一段代码块。
* `dialog`：用于表达人与人之间的对话，该元素包含 dt 和 dd 这两个组合元素， dt 用于表示说话者，而 dd 用来表示说话内容。
行内语义性元素主要完成web页面具体内容的引用和描述，是丰富内容展示的基础。
* `meter`：表示特定范围内的数值，可用于工资、数量、百分比等。
* `time`：表示时间值。
* `progress`：用来表示进度条，可通过对其 max 、 min 、 step 等属性进行控制，完成对进度的表示和监事。
* `video`：视频元素，用于支持和实现视频文件的直接播放，支持缓冲预载和多种视频媒体格式。
* `audio`：音频元素，用于支持和实现音频文件的直接播放，支持缓冲预载和多种音频媒体格式。
交互性元素主要用于功能性的内容表达，会有一定的内容和数据的关联，是各种事件的基础。
* `details`：用来表示一段具体的内容，但是内容默认可能不显示，通过某种手段（如单击）与 legend 交互才会显示出来。
* `datagrid`：用来控制客户端数据与显示，可以由动态脚本及时更新。
* `menu`：主要用于交互菜单（曾被废弃又被重新启用的元素）。
* `command`：用来处理命令按钮。

### 5.你做的网页在哪些流览器测试过,这些浏览器的内核分别是什么?
* IE: `trident` 内核
* Firefox: `gecko` 内核
* Safari: `webkit` 内核
* Opera: 以前是 presto 内核， Opera 现已改用 `Google Chrome` 的 `Blink` 内核
* Chrome:`Blink`( 基于 webkit ， Google 与 Opera Software 共同开发 )

### 6. 每个HTML文件里开头都有个很重要的东西，Doctype，知道这是干什么的吗？
声明位于文档中的最前面的位置，处于标签之前。此标签可告知浏览器文档使用哪种 HTML 或 XHTML 规范。（**重点：告诉浏览器按照何种规范解析页面**）

### 7.说说你对HTML5认识?（是什么,为什么）
**是什么：**
HTML5指的是包括 HTML 、 CSS 和 JavaScript 在内的一套技术组合。它希望能够减少网页浏览器对于需要插件的丰富性网络应用服务（ Plug-in-Based Rich Internet Application ， RIA ），例如： AdobeFlash 、 Microsoft Silverlight 与 Oracle JavaFX 的需求，并且提供更多能有效加强网络应用的标准集。 HTML5 是 HTML 最新版本， 2014 年 10 月由万维网联盟（ W3C ）完成标准制定。目标是替换 1999 年所制定的 HTML 4.01 和 XHTML 1.0 标准，以期能在互联网应用迅速发展的时候，使网络标准达到匹配当代的网络需求。

**为什么:**
HTML4陈旧不能满足日益发展的互联网需要，特别是移动互联网。为了增强浏览器功能 Flash 被广泛使用，但安全与稳定堪忧，不适合在移动端使用（耗电、触摸、不开放）。
HTML5增强了浏览器的原生功能，符合 HTML5 规范的浏览器功能将更加强大，减少了 Web 应用对插件的依赖，让用户体验更好，让开发更加方便，另外 W3C 从推出 HTML4.0 到 5.0 之间共经历了 17 年， HTML 的变化很小，这并不符合一个好产品的演进规则。

### 8.对WEB标准以及W3C的理解与认识?
1. 标签闭合、标签小写、不乱嵌套、提高搜索机器人搜索几率、使用外链css和 js 脚本、结构行为表现的分离，
2. 文件下载与页面速度更快、内容能被更多的用户所访问、内容能被更广泛的设备所访问、更少的代码和组件，
3. 容易维护、改版方便，不需要变动页面内容、提供打印版本而不需要复制内容、提高网站易用性。

### 9.HTML5行内元素有哪些,块级元素有哪些, 空元素有哪些?

**行内元素**
* a - 锚点
* abbr - 缩写
* acronym - 首字
* b - 粗体 ( 不推荐 )
* bdo - bidi override
* big - 大字体
* br - 换行
* cite - 引用
* code - 计算机代码 ( 在引用源码的时候需要 )
* dfn - 定义字段
* em - 强调
* font - 字体设定 ( 不推荐 )
* i - 斜体
* img - 图片
* input - 输入框
* kbd - 定义键盘文本
* label - 表格标签
* q - 短引用
* s - 中划线 ( 不推荐 )
* samp - 定义范例计算机代码
* select - 项目选择
* small - 小字体文本
* span - 常用内联容器，定义文本内区块
* strike - 中划线
* strong - 粗体强调
* sub - 下标
* sup - 上标
* textarea - 多行文本输入框
* tt - 电传文本
* u - 下划线
* var - 定义变量

**块元素 (block element)**
* address - 地址
* blockquote - 块引用
* center - 举中对齐块
* dir - 目录列表
* div - 常用块级容易，也是 css layout 的主要标签
* dl - 定义列表
* fieldset - form控制组
* form - 交互表单
* h3 - 大标题
* h4 - 副标题
* h3 - 3级标题
* h4 - 4级标题
* h5 - 5级标题
* h6 - 6级标题
* hr - 水平分隔线
* isindex - input prompt
* menu - 菜单列表
* noframes - frames可选内容，（对于不支持 frame 的浏览器显示此区块内容
* noscript - ）可选脚本内容（对于不支持 script 的浏览器显示此内容）
* ol - 排序表单
* p - 段落
* pre - 格式化文本
* table - 表格
* ul - 非排序列表

**可变元素**
> 可变元素为根据上下文语境决定该元素为块元素或者内联元素。
* applet - java applet
* button - 按钮
* del - 删除文本
* iframe - inline frame
* ins - 插入的文本
* map - 图片区块 (map)
* object - object对象
* script - 客户端脚本

**空元素**
>在 HTML[1] 元素中，没有内容的 HTML 元素被称为空元素
* `br`
* `hr`
* `input`
* `img`
* `link` 
* `meta`

### 10.什么是WebGL,它有什么优点?
WebGL（全写 Web Graphics Library ）是一种 3D 绘图标准，这种绘图技术标准允许把 JavaScript 和 OpenGL ES 2.0 结合在一起，通过增加OpenGL ES 2.0 的一个 JavaScript 绑定， WebGL 可以为 HTML5 Canvas 提供硬件 3D 加速渲染，这样 Web 开发人员就可以借助系统显卡来在浏览器里更流畅地展示 3D 场景和模型了，还能创建复杂的导航和数据视觉化。显然， WebGL 技术标准免去了开发网页专用渲染插件的麻烦，可被用于创建具有复杂 3D 结构的网站页面，甚至可以用来设计 3D 网页游戏等等。

WebGL完美地解决了现有的 Web 交互式三维动画的两个问题：
* 第一，它通过HTML脚本本身实现 Web 交互式三维动画的制作，无需任何浏览器插件支持 ;
* 第二，它利用底层的图形硬件加速功能进行的图形渲染，是通过统一的、标准的、跨平台的OpenGL接口实现的。
通俗说WebGL中 canvas 绘图中的 3D 版本。因为原生的 WebGL 很复杂，我们经常会使用一些三方的库，如 three.js 等，这些库多数用于HTML5 游戏开发。

### 11.请你描述一下 cookies，sessionStorage 和 localStorage 的区别?
`sessionStorage` 和 `localStorage` 是 `HTML5 Web Storage API` 提供的，可以方便的在 web 请求之间保存数据。有了本地数据，就可以避免数据在浏览器和服务器间不必要地来回传递。
`sessionStorage、` `localStorage` 、 `cookie` 都是在浏览器端存储的数据，其中 `sessionStorage` 的概念很特别，引入了一个“浏览器窗口”的概念。

 **sessionStorage** 是在**同源的同窗口**中，始终存在的数据。也就是说只要这个浏览器窗口没有关闭，即使刷新页面或进入同源另一页面，数据仍然存在。**关闭窗口后， sessionStorage 即被销毁**。同时“独立”打开的不同窗口，即使是同一页面， sessionStorage 对象也是不同的
**cookies会发送到服务器端。其余两个不会。**
Microsoft 指出 Internet Explorer 8 增加 cookie 限制为每个域名 50 个，但 IE7 似乎也允许每个域名 50 个 cookie 。 Firefox 每个域名 cookie 限制为 50 个。 Opera 每个域名 cookie 限制为 30 个。 Firefox 和 Safari 允许 cookie 多达 4097 个字节，包括名（ name ）、值（ value ）和等号。 Opera 许 cookie 多达 4096 个字节，包括：名（ name ）、值（ value ）和等号。 Internet Explorer 允许 cookie 多达 4095 个字节，包括：名（ name ）、值（ value ）和等号。

**区别：**

**Cookie**
1. 每个域名存储量比较小（各浏览器不同，大致 4K ）
2. 所有域名的存储量有限制（各浏览器不同，大致 4K ）
3. 有个数限制（各浏览器不同）
4. 会随请求发送到服务器

**LocalStorage**
1. 永久存储
2. 单个域名存储量比较大（推荐 5MB ，各浏览器不同）
3. 总体数量无限制

**SessionStorage**
1. 只在 Session 内有效
2. 存储量更大（推荐没有限制，但是实际上各浏览器也不同）

### 12.说说你对HTML语义化的理解?
* 什么是 HTML 语义化？

根据内容的结构化（内容语义化），选择合适的标签（代码语义化）便于开发者阅读和写出更优雅的代码的同时让浏览器的爬虫和机器很好地解析。
      **基本上都是围绕着几个主要的标签，像标题（ H1~H6 ）、列表（ li ）、强调（ strong em ）等等**

* 为什么要语义化？

1. 为了在没有CSS的情况下，页面也能呈现出很好地内容结构、代码结构 : 为了裸奔时好看；
2. 用户体验：例如title、 alt 用于解释名词或解释图片信息、 label 标签的活用；
3. 有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；
4. 方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；
5. 便于团队开发和维护，语义化更具可读性，是下一步吧网页的重要动向，遵循W3C标准的团队都遵循这个标准，可以减少差异化。

 语义化标签

* `<header></header>`
* `<footer></footer>`
* `<nav></nav>`
* `<section></section>`
* `<article></article>` SM:用来在页面中表示一套结构完整且独立的内容部分
* `<aslde></aside>` SM:主题的附属信息 ( 用途很广，主要就是一个附属内容 ) ，如果 article 里面为一篇文章的话，那么文章的作者以及信息内容就是这篇文章的附属内容了
* `<figure></figure>` SM:媒体元素，比如一些视频，图片啊等等
* `<datalist></datalist>`SM:选项列表，与 input 元素配合使用，来定义 input 可能的值
* `<details></details>`SM:用于描述文档或者文档某个部分的细节 ~ 默认属性为 open~
ps:配合 summary 一起使用

### 13.link和@import的区别?
```html
<link rel='stylesheet' rev='stylesheet' href='CSS文件 ' type='text/css' media='all' />
```
```
<style type='text/css' media='screen'>
    @import url('CSS文件 ');
</style>
```
两者都是外部引用CSS的方式，但是存在一定的区别：
*  `link` 是 XHTML 标签，除了加载 `CSS` 外，还可以定义` RSS` 等其他事务； `@import `属于 CSS 范畴，只能加载 CSS 。
* `link` 引用 CSS 时，在页面载入时同时加载；` @import `需要页面网页完全载入以后加载。
* `link` 是 XHTML 标签，无兼容问题； `@import` 是在 CSS2.1 提出的，低版本的浏览器不支持。
* `link` 支持使用 Javascript 控制 DOM 去改变样式；而 `@import` 不支持。

### 14.说说你对SVG理解?
`SVG可缩放矢量图形（ Scalable Vector Graphics ）`是基于可扩展标记语言（ XML ），用于描述二维矢量图形的一种图形格式。 SVG 是W3C('World Wide Web ConSortium' 即 ' 国际互联网标准组织 ') 在 2000 年 8 月制定的一种新的`二维矢量图形格式`，也是规范中的网络矢量图形标准。 SVG 严格遵从 XML 语法，并用文本格式的描述性语言来描述图像内容，因此是一种和图像分辨率无关的矢量图形格式。 SVG 于 2003 年 1 月14 日成为 W3C 推荐标准。

特点：
1. **任意放缩**。用户可以任意缩放图像显示，而不会破坏图像的清晰度、细节等。
2. **文本独立**。SVG图像中的文字独立于图像，文字保留可编辑和可搜寻的状态。也不会再有字体的限制，用户系统即使没有安装某一字体，也会看到和他们制作时完全相同的画面。
3. **较小文件**。总体来讲，SVG文件比那些 GIF 和 JPEG 格式的文件要小很多，因而下载也很快。
4. **超强显示效果**。SVG图像在屏幕上总是边缘清晰，它的清晰度适合任何屏幕分辨率和打印分辨率。
5. **超级颜色控制**。SVG图像提供一个 1600 万种颜色的调色板，支持 ICC 颜色描述文件标准、 RGB 、线 X 填充、渐变和蒙版。
6. **交互 X 和智能化**。 SVG 面临的主要问题一个是如何和已经占有重要市场份额的矢量图形格式 Flash 竞争的问题，另一个问题就是 SVG 的本地运行环境下的厂家支持程度。
7. **浏览器支持**
Internet Explorer9，火狐，谷歌 Chrome ， Opera 和 Safari 都支持 SVG 。
IE8和早期版本都需要一个插件 - 如 Adobe SVG 浏览器，这是免费提供的。

### 15.HTML全局属性(global attribute)有哪些?
`MDN`: `html global attribute`或者`W3C HTML global-attributes accesskey`:设置快捷键，提供快速访问元素如`aaa`在`windows`下的`firefox`中按`alt + shift + a`可激活元素 class:为元素设置类标识，多个类名用空格分开，CSS和javascript可通过class属性获取元素 contenteditable: 指定元素内容是否可编辑 contextmenu: 自定义鼠标右键弹出菜单内容 data-*: 为元素增加自定义属性 dir: 设置元素文本方向 draggable: 设置元素是否可拖拽 dropzone: 设置元素拖放类型： copy, move, link hidden: 表示一个元素是否与文档。样式上会导致元素不显示，但是不能用这个属性实现样式效果 id: 元素id，文档内唯一 lang: 元素内容的的语言 spellcheck: 是否启动拼写和语法检查 style: 行内css样式 tabindex: 设置元素可以获得焦点，通过tab可以导航 title: 元素相关的建议信息 translate: 元素和子孙节点内容是否需要本地化

### 16.说说超链接target属性的取值和作用？
`target`这个属性指定所链接的页面在浏览器窗口中的打开方式。

它的参数值主要有：
1. ` _blank` ：在新浏览器窗口中打开链接文件
2. ` _parent` ：将链接的文件载入含有该链接框架的父框架集或父窗口中。如果含有该链接的框架不是嵌套的，则在浏览器全屏窗口中载入链接的文件，就象 _self 参数。
3. `_self` ：在同一框架或窗口中打开所链接的文档。此参数为默认值，通常不用指定。
4. ` _top` ：在当前的整个浏览器窗口中打开所链接的文档，因而会删除所有框架。

### 17.data-属性的作用是什么？
`data-xxx`为前端开发者提供**自定义的属性**，这些属性集可以通过对象的 `dataset`属性获取，不支持该属性的浏览器可以通过 `getAttribute`方法获取。

需要注意的是：`data-xxx`之后的以连字符分割的多个单词组成的属性，获取的时候使用**驼峰风格**。并不是所有的浏览器都支持`.dataset 属性`，测试的浏览器中只有 Chrome 和 Opera 支持。
即：当没有合适的属性和元素时，自定义的 data 属性是能够存储页面或 App 的私有的自定义数据。

### 18.介绍一下你对浏览器内核的理解？
浏览器内核主要分成两部分：**`渲染引擎(layout engineer或 Rendering Engine)`** 和** `JS引擎`**。

**渲染引擎**：负责取得网页的内容（HTML、 XML 、图像等等）、整理讯息（例如加载 CSS 等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。
**JS引擎**：解析和执行 javascript 来实现网页的动态效果。

最开始渲染引擎和JS引擎并没有区分的很明确，后来 JS 引擎越来越独立，内核就倾向于只指渲染引擎。

### 19.常见的浏览器内核有哪些？
1. `Trident内核`： `IE`,`MaxThon`,`TT`,`The World`,`360`, `搜狗`等。[ 又称 MSHTML]
2. `Gecko内核`： `Netscape6` 及以上版本，`FF`,`MozillaSuite/SeaMonkey `等
3. `Presto内核`： `Opera7 `及以上。[`Opera` 内核原为： `Presto` ，现为：` Blink`;]
4. `Webkit内核`： `Safari`,`Chrome` 等。[ `Chrome` 的： `Blink （ WebKit 的分支）` ]

### 20.iframe有那些缺点？
1. `iframe`会阻塞主页面的 `Onload` 事件； 
2. 搜索引擎的检索程序无法解读这种页面，不利于 `SEO`;
3. `iframe` 和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。
***
>使用`iframe`之前需要考虑这两个缺点。如果需要使用 `iframe`，最好是**通过 javascript动态给iframe添加 src 属性值**，这样可以绕开以上两个问题。

### 21.Label的作用是什么，是怎么用的？
`label`标签来*定义表单控制间的关系* , 当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。

```html
<label for='Name'>Number:</label>
<input type=“ text “ name='Name' id='Name'/>
<label>Date:<input type='text' name='B'/></label>
```

### 22.如何实现浏览器内多个标签页之间的通信?
`WebSocket`、 `SharedWorker `，也可以调用`localstorge`、 `cookies` 等本地存储方式；
`localstorge` 另一个浏览上下文里被添加、修改或删除时，它都会触发一个事件，我们通过监听事件，控制它的值来进行页面信息通信；
 
注意quirks： `Safari` 在无痕模式下设置 `localstorge` 值时会抛出 `QuotaExceededError` 的异常；

### 23.如何在页面上实现一个圆形的可点击区域？
1. map+area(锚点图) 或者 svg
2. `border-radius`
3. 纯 js 实现 需要求一个点在不在圆上简单算法、获取鼠标坐标等等

### 24.title与h3的区别、b与strong的区别、i与em的区别？

* `title`属性没有明确意义只表示是个标题， `H1` 则表示层次明确的标题，对页面信息的抓取也有很大的影响；
* `strong`是标明重点内容，有语气加强的含义，使用阅读设备阅读网络时： 会重读，而 `<B> `是展示强调内容。
* `i`内容展示为斜体， `em` 表示强调的文本；

* Physical Style Elements -- 自然样式标签
b, i, u, s, pre
* Semantic Style Elements -- 语义样式标签
strong, em, ins, del, code
*应该准确使用语义样式标签, 但不能滥用 , 如果不能确定时首选使用自然样式标签。*

### 25.实现不使用 border 画出1px高的线，在不同浏览器的标准模式与怪异模式下都能保持一致的效果？

```html
<div style='height:1px;overflow:hidden;background:red'></div>
```

### 26.HTML5标签的作用?(用途)
1. 使Web页面的内容更加有序和规范
2. 使搜索引擎更加容易按照HTML5规则识别出有效的内容
3. 使Web页面更接近于一种数据字段和表

### 27.简述一下src与href的区别？
`src`用于替换当前元素， `href` 用于在当前文档和引用资源之间确立联系。

`src`是 source 的缩写，指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置；在请求 `src` 资源时会将其指向的资源下载并应用到文档内，例如 `js脚本` ， `img图片`和 `frame` 等元素。

```html
<script src ='js.js'></script>
```

当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，图片和框架等元素也如此，类似于将所指向资源嵌入当前标签内。这也是为什么将js脚本放在底部而不是头部。

`href`是 `Hypertext Reference` 的缩写，指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，如果我们在文档中添加
`<link href='common.css' rel='stylesheet'/>`，那么浏览器会识别该文档为css文件，就会并行下载资源并且不会停止对当前文档的处理。这也是为什么建议使用 link 方式来加载 css ，而不是使用@import 方式。

### 28.谈谈你对canvas的理解？
canvas是HTML5中新增一个HTML5标签与操作canvas的javascript API，它可以实现在网页中完成动态的2D与3D图像技术。标记和 SVG以及 VML 之间的一个重要的不同是，有一个基于 JavaScript 的绘图 API，而 SVG 和 VML 使用一个 XML 文档来描述绘图。SVG 绘图很容易编辑与生成，但功能明显要弱一些。 canvas可以完成动画、游戏、图表、图像处理等原来需要Flash完成的一些功能。

### 29.WebSocket与消息推送？
B/S架构的系统多使用HTTP协议

HTTP协议的特点： 1. 无状态协议 2. 用于通过 Internet 发送请求消息和响应消息 3. 使用端口接收和发送消息，默认为80端口 底层通信还是使用Socket完成。

HTTP协议决定了服务器与客户端之间的连接方式，无法直接实现消息推送（ F5 已坏）
一些变相的解决办法：
双向通信与消息推送
轮询：客户端定时向服务器发送Ajax请求，服务器接到请求后马上返回响应信息并关闭连接。
优点：后端程序编写比较容易。
缺点：请求中有大半是无用，浪费带宽和服务器资源。
实例：适于小型应用。
长轮询：客户端向服务器发送Ajax请求，服务器接到请求后 hold 住连接，直到有新消息才返回响应信息并关闭连接，客户端处理完响应信息后再向服务器发送新的请求。
优点：在无消息的情况下不会频繁的请求，耗费资小。
缺点：服务器hold连接会消耗资源，返回数据顺序无保证，难于管理维护。 Comet 异步的 ashx ，
实例：WebQQ、 Hi 网页版、 Facebook IM 。
长连接：在页面里嵌入一个隐蔵iframe，将这个隐蔵 iframe 的 src 属性设为对一个长连接的请求或是采用 xhr 请求，服务器端就能源源不断地往客户端输入数据。
优点：消息即时到达，不发无用请求；管理起来也相对便。
缺点：服务器维护一个长连接会增加开销。
实例：Gmail聊天
Flash Socket：在页面中内嵌入一个使用了 Socket 类的 Flash 程序 JavaScript 通过调用此 Flash 程序提供的 Socket 接口与服务器端的 Socket 接口进行通信， JavaScript 在收到服务器端传送的信息后控制页面的显示。
优点：实现真正的即时通信，而不是伪即时。
缺点：客户端必须安装Flash插件；非 HTTP 协议，无法自动穿越防火墙。
实例：网络互动游戏。
Websocket:
WebSocket是 HTML5 开始提供的一种浏览器与服务器间进行全双工通讯的网络技术。依靠这种技术可以实现客户端和服务器端的长连接，双向实时通信。
特点:
a、事件驱动
b、异步
c、使用 ws 或者 wss 协议的客户端 socket
d、能够实现真正意义上的推送功能
缺点：少部分浏览器不支持，浏览器支持的程度与方式有区别。

### 30.img的title和alt有什么区别？
* `alt` 用于图片无法加载时显示
* `title` 为该属性提供信息，通常当鼠标滑动到元素上的时候显示

### 31.表单的基本组成部分有哪些，表单的主要用途是什么？
组成：表单标签、表单域、表单按钮

1. 表单标签：这里面包含了处理表单数据所用 CGI 程序的 URL, 以及数据提交到服务器的方法。
2. 表单域：包含了文本框、密码框、隐藏域、多行文本框、复选框、单选框、下拉选择框、和文件上传框等。
3. 表单按钮：包括提交按钮，复位按钮和一般按钮；用于将数据传送到服务器上的 CGI 脚本或者取消输入，还可以用表单按钮来控制其他定义了处理脚本的处理工作。
主要用途：表单在网页中主要负责数据采集的功能，和向服务器传送数据。

### 32.表单提交中Get和Post方式的区别？
1. get 是从服务器上获取数据， post 是向服务器传送数据。
2.  get 是把参数数据队列加到提交表单的 ACTION 属性所指的 URL 中，值和表单内各个字段一一对应，在 URL 中可以看到。 post 是通过 HTTP post 机制，将表单内各个字段与其内容放置在 HTML HEADER 内一起传送到 ACTION 属性所指的 URL 地址 , 用户看不到这个过程。
3. 对于 get 方式，服务器端用 Request.QueryString 获取变量的值，对于 post 方式，服务器端用 Request.Form 获取提交的数据。
4. get 传送的数据量较小，不能大于 2KB 。 post 传送的数据量较大，一般被默认为不受限制。但理论上， IIS4 中最大量为 80KB ， IIS5 中为100KB 。
5.  get 安全性非常低， post 安全性较高。

### 33.HTML5 有哪些新增的表单元素？
HTML5 新增了很多表单元素让开发者构建更优秀的 Web 应用程序。

* datalist
* datetime
* output
* keygen
* date
* month
* week
* time
* color
* number
* range
* email
* Url

### 34.HTML5 废弃了哪些 HTML4 标签？
HTML5 废弃了一些过时的，不合理的HTML 标签：
* frame
* frameset
* noframe
* applet
* big
* center
* basefront

### 35.HTML5 标准提供了哪些新的 API？
HTML5 提供的应用程序 API 主要有：
* Media API
* Text Track API
* Application Cache API
* User Interaction
* Data Transfer API
* Command API
* Constraint Validation API
* History API

### 36.HTML5 存储类型有什么区别？
HTML5 能够本地存储数据，在之前都是使用 cookies 使用的。 HTML5 提供了下面两种本地存储方案：
* localStorage 用于持久化的本地存储，数据永远不会过期，关闭浏览器也不会丢失。
* sessionStorage 同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此sessionStorage不是一种持久化的本地存储，仅仅是会话级别的存储

### 37.HTML5 应用程序缓存和浏览器缓存有什么区别？
**应用程序缓存**是 HTML5 的重要特性之一，提供了离线使用的功能，让应用程序可以获取本地的网站内容，例如 HTML 、 CSS 、图片以及 JavaScript 。这个特性可以提高网站性能，它的实现借助于 manifest 文件，如下：
```html
<!doctype html>
<html manifest=”example.appcache”>
    <!-- ... -->
</html>
```
与传统浏览器缓存相比，它不强制用户访问的网站内容被缓存。

### 38.HTML5 Canvas 元素有什么用？

Canvas 元素用于在网页上绘制图形，该元素标签强大之处在于可以直接在 HTML 上进行图形操作
```js
<canvas id=” canvas1 ″ width= ” 300 ″ height= ” 100 ″ >
</canvas>
```

### 39.除了 audio 和 video，HTML5 还有哪些媒体标签？
>HTML5 对于多媒体提供了强有力的支持，除了 audio 和 video 标签外，还支持以下标签：
* <embed> 标签定义嵌入的内容，比如插件。
`<embed type=” video/quicktime ” src= ” Fishing.mov ” >`
* <source> 对于定义多个数据源很有用。
```
<video width=” 450 ″ height= ” 340 ″ controls>
  <source src=” jamshed.mp4 ″ type= ” video/mp4 ″ >
  <source src=” jamshed.ogg ” type= ” video/ogg ” >
</video>
```
* <track> 标签为诸如 video 元素之类的媒介规定外部文本轨道。 用于规定字幕文件或其他包含文本的文件，当媒介播放时，这些文件是可见的。
```
<video width=” 450 ″ height= ” 340 ″ controls>
    <source src=” jamshed.mp4 ″ type= ” video/mp4 ″ >
    <source src=” jamshed.ogg ” type= ” video/ogg ” >
    <track kind=” subtitles ” label= ” English ” src= ” jamshed_en.vtt ” srclang= ” en ” default></track>
    <track kind=” subtitles ” label= ” Arabic ” src= ” jamshed_ar.vtt ” srclang= ” ar ” ></track>
</video>
```
据源很有用。标签为诸如 video 元素之类的媒介规定外部文本轨道。 用于规定字幕文件或其他包含文本的文件，当媒介播放时，这些文件是可见的。

### 40.HTML5 中如何嵌入视频？
>和音频类似，HTML5 支持 MP4 、 WebM 和 Ogg 格式的视频，下面是简单示例：
```
<video width=” 450 ″ height= ” 340 ″ controls>
    <source src=” jamshed.mp4 ″ type= ” video/mp4 ″ >
    Your browser does’ nt support video embedding feature.
</video>
```

### 4.HTML5 中如何嵌入音频？
>HTML5 支持 MP3 、 Wav 和 Ogg 格式的音频，下面是在网页中嵌入音频的简单示例：
```
<audio controls>
    <source src=” jamshed.mp3 ″ type= ” audio/mpeg ” >
    Your browser does’ nt support audio embedding feature.
</audio>
```

### 42 .新的 HTML5 文档类型和字符集是？
>HTML5 文档类型很简单：
```
<!doctype html>
<!--HTML5 使用 UTF-8 编码示例-->
<meta charset=” UTF-8 ″ >
```

### 43.解释一下CSS的盒子模型？
1. **标准的css盒子模型**：宽度=内容的宽度+边框的宽度+加上内边具的宽度
2. 网页设计中常听的属性名：内容(content)、填充(padding)、边框(border)、边界(margin)， CSS盒子模式都具备这些属性。
3. 这些属性我们可以把它转移到我们日常生活中的盒子（箱子）上来理解，日常生活中所见的盒子也就是能装东西的一种箱子，也具有这些属性，所以叫它盒子模式。CSS盒子模型就是在网页设计中经常用到的CSS技术所使用的一种思维模型。

盒子模型也有人称为框模型，HTML中的多数元素都会在浏览器中生成一个矩形的区域，每个区域包含四个组成部分，从外向内依次是：外边距（Margin）、边框（Border）、内边距（Padding）和内容（Content），其实盒子模型有两种，分别是 ie 盒子模型和标准 w3c 盒子模型，加上了doctype声明，让所有浏览器都会采用标准 w3c 盒子模型去解释你的盒子。

### 44. 请你说说CSS选择器的类型有哪些，并举几个例子说明其用法？
类型：基础的选择器、组合选择器、属性选择器、伪类、伪元素

### 45.请你说说CSS有什么特殊性?（优先级、计算特殊值）
**优先级**

1. 同类型，同级别的样式后者先于前者
2. ID > 类样式 > 标签 > 
3. 内联>ID选择器>伪类>属性选择器>类选择器>标签选择器>通用选择器()>继承的样式
4. 具体 > 泛化的，特殊性即css优先级
5. 近的 > 远的 (内嵌样式 > 内部样式表 > 外联样式表)
  **内嵌样式**：内嵌在元素中，<span style="color:red">span</span>
  **内部样式表**：在页面中的样式，写在<style></style>中的样式
**外联样式表**：单独存在一个css文件中，通过link引入或import导入的样式
6. !important 权重最高，比 inline style 还要高

**计算特殊性值**

> important > 内嵌 > ID > 类 > 标签 | 伪类 | 属性选择 > 伪对象 > 继承 > 通配符

权重、特殊性计算法：CSS样式选择器分为4个等级，a、b、c、d
1. 如果样式是行内样式（通过Style=“”定义），那么a=1，1,0,0,0
2. b为ID选择器的总数 0,1,0,0
3. c为属性选择器，伪类选择器和class类选择器的数量。0,0,1,0
4. d为标签、伪元素选择器的数量 0,0,0,1
5. `!important` 权重最高，比 `inline style` 还要高
比如结果为：1093比1100，按位比较，从左到右，只要一位高于则立即胜出，否则继续比较。

### 46.要动态改变层中内容可以使用的方法？
innerHTML，innerText