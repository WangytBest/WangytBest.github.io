---
title: sass基础入门
date: 2018-04-03 20:39:08
categories: [CSS]
toc: true
tags: CSS
---

## css功能拓展

### 嵌套（Nested Rules）
sass允许将css样式嵌套进另一套样式中，内层的样式将他的外层的选择器作为父选择器。
### 父选择器 & (Referencing Parent Selectors: &)
### 属性嵌套 (Nested Properties)
```css
.funky {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
```
### 占位符选择器 %foo (Placeholder Selectors: %foo)
<!-- more -->
## SassScript

### 变量 $ (Variables: $)
```css
$width: 5em;

#main {
    width: $width;
}
```

变量支持块级作用域，嵌套规则内定义的变量只能在嵌套规则内使用（局部变量），不在嵌套规则内定义的变量则可在任何地方使用（全局变量）。将局部变量转换为全局变量可以添加 `!global` 声明
```css
#main {
    $width: 5em !global;
    width: $width;
}

#sidebar {
    width: $width;
}
```