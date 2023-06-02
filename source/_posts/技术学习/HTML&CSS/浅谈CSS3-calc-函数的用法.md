---
title: 浅谈CSS3 calc()函数的用法
tags:
  - 前端
categories:
  - 技术学习
  - HTML&CSS
copyright: false
abbrlink: '28661195'
cover: '/assets/img/post/css.webp'
date: 2021-12-03 22:23:23
---

CSS3 的 `calc()` 函数允许我们在属性值中执行数学计算操作。例如，我们可以使用 `calc()` 指定一个元素宽的固定像素值为多个数值的和。

```css
.foo {
  width: calc(100px + 50px);
}
```

## 为什么是 `calc()`

如果你使用过 CSS 预处理器，比如 SASS，以上示例你或许碰到过

```css
.foo {
    width: 100px + 50px;
}

// Or using SASS variables
$width-one: 100px;
$width-two: 50px;
.bar {
    width: $width-one + $width-two;
}
```

然而，`calc()` 函数提供了更好的解决方案。首先，我们能够组合不同的单元。特别是，我们可以混合计算绝对单元（比如百分比与视口单元）与相对单元（比如像素）。例如，我们可以创造一个表达式，用一个百分比减掉一个像素值。

```css
.foo {
    width: calc(100% - 50px);
}
```

本例中，`.foo` 元素总是小于它父元素宽度 50px。 第二，使用 `calc()`，计算值是表达式它自己，而非表达式的结果。当使用 CSS 预处理器做数学运算时，给定值为表达式的结果。

```scss
// Value specified in SCSS
.foo {
    width: 100px + 50px;
}

// Compiled CSS and computed value in browser
.foo {
    width: 150px;
}
```

然而，浏览器解析的 `calc()` 的值为真实的 `calc()` 表达式。

```css
// Value specified in CSS
.foo {
    width: calc(100% - 50px);
}

// Computed value in browser
.foo {
    width: calc(100% - 50px);
}
```

这意味着浏览器中的值可以更加灵活，能够响应视口的改变。我们能够给元素设定一个高度为视口的高度减去一个绝对值，它将随视口的改变进行调节。

## 使用 `calc()`

`calc()` 函数可以用来对数值属性执行四则运算。比如，`<length>`，`<frequency>`，`<angle>`，`<time>`，`<number>` 或者 `<integer` [数据类型](https://bitsofco.de/generic-css-data-types/) 这里有一些示例：

```css
.foo {
    width: calc(50vmax + 3rem);
    padding: calc(1vw + 1em);
    transform: rotate( calc(1turn + 28deg) );
    background: hsl(100, calc(3 * 20%), 40%);
    font-size: calc(50vw / 3);
}
```

## `clac()` 嵌套

`calc()` 函数可以嵌套。在函数里边，会被视为简单的括号表达式，如下例所示。

```css
.foo {
    width: calc( 100% / calc(100px * 2) );
}
```

函数的计算值如下所示：

```css
.foo {
    width: calc( 100% / (100px * 2) );
}
```

## 一个垫片

`clac()` 已经得到普遍支持。 ![t018a953fa8d7f2ad29](http://caibaojian.com/d/uploads/2017/05/t018a953fa8d7f2ad29.png) 对于不支持 `calc()` 的浏览器，整个属性值表达式将被忽略。不过我们可以对那些不支持 `calc()`的浏览器，使用一个固定值作为回退。

```css
.foo {
    width: 90%; /* Fallback for older browsers */
    width: calc(100% - 50px);
}
```

## 什么场景可以使用 `calc()`

### Example 1 - 居中元素

使用 `calc()` 给我们提供另一个垂直居中元素的解决方案。如果我们知道元素的尺寸，一个典型的解决方案是使用负外边距移动自身距离高与宽的一半，如下所示：

```css
// Assuming .foo is 300px height and 300px width
.foo {
    position: absolute
    top: 50%;
    left: 50%;
    marging-top: -150px;
    margin-left: -150px;
}
```

使用 `calc()` 函数，我们仅仅通过 top 与 left 属性便能实现相同的效果：

```css
.foo {
    position: absolute
    top: calc(50% - 150px);
    left: calc(50% - 150px);
}
```

Flexbox 的介入，已经很少需要这种方法了。不过，一些情况下 Flexbox 不能被使用。比如，元素需要绝对定位或者固定定位，这种方法是有用的。

### Example 2 - 创建根栅格尺寸

使用 `rem`，`calc()` 函数能够用来创建一个基于视口的栅格。我们可以设置根元素的字体大小为视口宽度的一部分。

```css
html {  
    font-size: calc(100vw / 30);
}
```

现在，`1rem` 为视口宽度的 1/30。在页面上的任何文本，将会根据你的视口自动缩放。更进一步，相同比例的视口总会显示相同的文本数量，不管视口的真实尺寸是多少。 ![t0155d1e9ed3a88bc68](http://caibaojian.com/d/uploads/2017/05/t0155d1e9ed3a88bc68.gif) 如果我们对非文本使用 `rem` 设置大小，它们同样遵守这个行为。一个 1rem 宽度的元素总是视口元素宽度的 1/30。

### Example 3 - 清晰

最后，`calc()`使计算更加清晰。如果你使一组项目为它们父元素容器宽度的 1/6，你可能值么写：

```css
.foo {
    width: 16.666666667%;
}
```

然而，它能够更加清晰并具有可读性：

```css
.foo {
    width: calc(100% / 6);
}
```

使用 `calc()`，我们还能做更多的事情，比如[创建一个栅格系统](https://www.sitepoint.com/creative-grid-system-sass-calc/)。它是 CSS 最有用的新特性之一。
