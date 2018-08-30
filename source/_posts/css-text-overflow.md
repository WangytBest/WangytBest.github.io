---
title: css控制文本内容溢出截断
date: 2017-10-19 10:39:12
tags: [css, text-overflow]
thumbnail: http://ow9cw9x3t.bkt.clouddn.com/nianshaodeni.png
---

css控制文字内容的溢出显示，溢出截断后末尾出现省略```...```，单行文本与多行文本的控制又有区别。

**单行文本**
```css
overfolw: hidden;
text-overflow: ellipsis;
white-space: nowrap;
```

**多行文本**
```css
display:-webkit-box;
-webkit-line-clamp: 1;
-webkit-box-orient: vertical;
overflow: hidden;
```

**知识点**

`text-overflow` 确定内容的溢出显示，可以被剪切(`clip`)、显示一个省略号（`...`）或者显示一个自定义字符串。

> * 需要设置`overflow: hidden`属性才能生效，否则不会强制溢出事件发生。
> * 属性只对**块级元素**溢出的内容有效，但必须与块级元素内联（`inline`）方向一致。如内容在盒子下方溢出，则属性不会生效。
> * 文本溢出：1、文本无法换行，设置了`white-space: nowrap;`。2、单词太长。 

```css
text-overflow: [ clip | ellipise | <string> ]{1, 2}
```

> 1. `clip`: 内容区域的极限处截断文本，因此可能在字符的中间可能会发生截断。**为了能够在两个字符过度处截断，必须使用一个空字符串值（` `）**。
> 2. `ellipse`: 用省略号`...`来表示截断的文本。如果空间太小连省略号也不能显示，那么省略号也会被截断。
> 3. `<string>`: `<string>`用来表示被截断的文本。字符串内容将被添加在内容区域中，所以会减少显示出的文本。如果空间太小到连省略号的容纳下，那么这个字符串也会被截断。

```css
/* Overflow behavior at line end
Right end if ltr, left end if rtl */
text-overflow: clip;
text-overflow: ellipsis;
text-overflow: "…";
text-overflow: fade;
text-overflow: fade(10px);
text-overflow: fade(5%);

/* Overflow behavior at left end | at right end
Directionality has no influence */
text-overflow: clip ellipsis;
text-overflow: "…" "…";
text-overflow: fade clip;
text-overflow: fade(10px) fade(10px);
text-overflow: fade(5%) fade(5%);

/* Global values */
text-overflow: inherit;
text-overflow: initial;
text-overflow: unset;
```

<style type="text/css">
    div br{
        display: none;
    }
</style>

<div>
    <table>
        <thead>
            <tr>
                <th colspan="1" rowspan="2" scope="col">CSS value</th>
                <th colspan="2" rowspan="1" scope="col"><code>direction: ltr</code></th>
                <th colspan="2" rowspan="1" scope="col"><code>direction: rtl</code></th>
            </tr>
            <tr>
                <th scope="col">Expected Result</th>
                <th scope="col">Live result</th>
                <th scope="col">Expected Result</th>
                <th scope="col">Live result</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td><em>visible overflow</em></td>
                <td>1234567890</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>0987654321</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: clip</code></td>
                <td><img src="https://developer.mozilla.org/@api/deki/files/6056/=t-o_clip.png" alt="t-o_clip.png"></td>
                <td>
                    <p>123456</p>
                </td>
                <td><img src="https://developer.mozilla.org/@api/deki/files/6057/=t-o_clip_rtl.png" alt="t-o_clip_rtl.png"></td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: ''</code></td>
                <td>12345</td>
                <td>
                    <p>123456</p>
                </td>
                <td>54321</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: ellipsis</code></td>
                <td>1234…</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>…4321</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: '.'</code></td>
                <td>1234.</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>.4321</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: clip clip</code></td>
                <td>123456</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>654321</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: clip ellipsis</code></td>
                <td>1234…</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>6543…</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: clip '.'</code></td>
                <td>1234.</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>6543.</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: ellipsis clip</code></td>
                <td>…3456</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>…4321</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: ellipsis ellipsis</code></td>
                <td>…34…</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>…43…</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: ellipsis '.'</code></td>
                <td>…34.</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>…43.</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: ',' clip</code></td>
                <td>,3456</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>,4321</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: ',' ellipsis</code></td>
                <td>,34…</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>,43…</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
            <tr>
                <td><code>text-overflow: ',' '.'</code></td>
                <td>,34.</td>
                <td>
                    <p>1234567890</p>
                </td>
                <td>,53.</td>
                <td>
                    <p>1234567890</p>
                </td>
            </tr>
        </tbody>
    </table>
</div>

