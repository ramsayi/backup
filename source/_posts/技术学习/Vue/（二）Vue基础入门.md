---
title: （二）Vue基础入门
tags:
  - Vue3
categories:
  - 技术学习
  - Vue
cover: '/assets/img/post/vuejs.webp'
abbrlink: 4f072fd7
date: 2022-04-21 21:55:55
---

# Vue简介

略

# Vue的基本使用

## 1.基本使用步骤

①导入vue.js的script脚本文件
②在页面中声明一个将要被Vue所控制的DOM区域
③创建vm实例对象(vue实例对象)

![image-20220421220323623](/assets/img/article/image-20220421220323623.png)

## 2.基本代码与MVVM的对应关系

![image-20220421220546485](/assets/img/article/image-20220421220546485.png)

# Vue的调试工具

略

# Vue的指令与过滤器

## 1.指令的概念

指令(Directives)是vue为开发者提供的模板语法，用于辅助开发者渲染页面的基本结构。

Vue中的指令按照不同的用途可以分为如下6大类：

① 内容渲染指令
② 属性绑定指令
③ 事件绑定指令
④ 双向绑定指令
⑤ 条件渲染指令
⑥ 列表渲染指令

注意：指令是Vue开发中最基础、最常用、最简单的知识点。

### 1.1内容渲染指令

内容渲染指令用来辅助开发者渲染DOM元素的文本内容。常用的内容渲染指令有如下3个：

- v-text

- `{{}}`
- v-html

#### `v-text`

用法示例

![image-20220421222159563](/assets/img/article/image-20220421222159563.png)

注意：v-text指令会覆盖元素内默认的值。

#### `{{}}`语法

vue提供的`{{}}`语法，专门用来解决v-text会覆盖默认文本内容的问题。这种`{{}}`语法的专业名称是插值表达式（英文名为：Mustache)。

![image-20220421223805888](/assets/img/article/image-20220421223805888.png)

注意：相对于v-text指令来说，插值表达式在开发中更常用一些！因为它不会覆盖元素中默认的文本内容。

#### `v-html`

v-text指令和插值表达式只能渲染纯文本内容。如果要把包含HTML标签的字符串渲染为页面的HTML元素，则需要用到v-html这个指令：

![image-20220421224643021](/assets/img/article/image-20220421224643021.png)

### 1.2属性绑定指令

如果需要为元素的属性动态绑定属性值，则需要用到v-bind属性绑定指令。用法示例如下：

![image-20220421225905587](/assets/img/article/image-20220421225905587.png)

#### 属性绑定指令的简写形式

由于v-bind指令在开发中使用频率非常高，因此，Vue官方为其提供了简写形式（简写为英文的`:`）。

![image-20220421230241804](/assets/img/article/image-20220421230241804.png)

#### 使用Javascript表达式

在vue提供的模板渲染语法中，除了支持绑定简单的数据值之外，还支持Javascript表达式的运算，例如：

![image-20220421231116942](/assets/img/article/image-20220421231116942.png)

### 1.3事件绑定指令

Vue提供了v-on事件绑定指令，用来辅助程序员为DOM元素绑定事件监听。语法格式如下：

![image-20220422110428560](/assets/img/article/image-20220422110428560.png)

注意：原生DOM对象有onclick、oninput、onkeyup等原生事件，替换为vue的事件绑定形式后，
分别为：v-on:click、v-on:input、v-on:keyup

通过v-on绑定的事件处理函数，需要在methods节点中进行声明：

![image-20220422110557008](/assets/img/article/image-20220422110557008.png)

#### 事件绑定的简写形式

由于v-on指令在开发中使用频率非常高，因此，vue官方为其提供了简写形式（简写为英文的`@`）

![image-20220422110743719](/assets/img/article/image-20220422110743719.png)

#### 事件对象event

在原生的DOM事件绑定中，可以在事件处理函数的形参处，接收事件对象event。同理，在v-on指令（简写为@)所绑定的事件处理函数中，同样可以接收到事件对象event,示例代码如下：

![image-20220422110831031](/assets/img/article/image-20220422110831031.png)

#### 绑定事件并传参

在使用v-on指令绑定事件时，可以使用`()`进行传参，示例代码如下：

![image-20220422110907957](/assets/img/article/image-20220422110907957.png)

#### $event

$event是vue提供的特殊变量，用来表示原生的事件参数对象event。$event可以解决事件参数对象event
被覆盖的问题。示例用法如下：

![image-20220422110950986](/assets/img/article/image-20220422110950986.png)

#### 事件修饰符

在事件处理函数中调用preventDefault()或stopPropagation()是非常常见的需求。因此，vue提供了事件修饰符的概念，来辅助程序员更方便的对事件的触发进行控制。常用的5个事件修饰符如下：

![image-20220422111132744](/assets/img/article/image-20220422111132744.png)

#### 按键修饰符

在监听键盘事件时，我们经常需要判断详细的按键。此时，可以为键盘相关的事件添加按键修饰符，例如：

![image-20220422111207293](/assets/img/article/image-20220422111207293.png)

### 1.4双向绑定指令

Vue提供了v-model双向数据绑定指令，用来辅助开发者在不操作DOM的前提下，快速获取表单的数据。

![image-20220422111328899](/assets/img/article/image-20220422111328899.png)

注意：v-model指令只能配合表单元素一起使用！

#### v-model指令的修饰符

为了方便对用户输入的内容进行处理，vue为v-model指令提供了3个修饰符，分别是：

![image-20220422111421380](/assets/img/article/image-20220422111421380.png)

### 1.5条件渲染指令

条件渲染指令用来辅助开发者按需控制DOM的显示与隐藏。条件渲染指令有如下两个，分别是：

- v-if
- v-show

#### v-if和v-show的区别

实现原理不同：

- v-if指令会动态地创建或移除DOM元素，从而控制元素在页面上的显示与隐藏；

- v-show指令会动态为元素添加或移除style="display:none;"样式，从而控制元素的显示与隐藏；


性能消耗不同：

- v-if有更高的切换开销，而v-show有更高的初始渲染开销。

- 如果需要非常频繁地切换，则使用v-show较好

- 如果在运行时条件很少改变，则使用v-if较好

#### v-else

v-if可以单独使用，或配合v-else指令一起使用：

![image-20220422164848208](/assets/img/article/image-20220422164848208.png)

#### v-else-if

v-else-if 指令，顾名思义，充当 v-if 的“else-if 块”，可以连续使用：

![image-20220422200541308](/assets/img/article/image-20220422200541308.png)

### 1.6 列表渲染指令

vue 提供了 v-for 指令，用来辅助开发者基于一个数组来循环
染相似的 UI 结构。
v-for 指令需要使用 item in items 的特殊语法，其中：

- items 是待循环的数组
- item 是当前的循环项

![image-20220422200745535](/assets/img/article/image-20220422200745535.png)

#### v-for 中的索引

v-for 指令还支持一个可选的第二个参数，即当前项的索引。语法格式为 (item, index) in items，示例代码如下：

![image-20220422200824270](/assets/img/article/image-20220422200824270.png)

注意：v-for指令中的item项和index索引都是形参，可以根据需要进行重命名。例如(user,i) in userlist

#### 使用key维护列表的状态

当列表的数据变化时，默认情况下，Vue会尽可能的复用已存在的DOM元素，从而提升渲染的性能。但这种默认的性能优化策略，会导致有状态的列表无法被正确更新。
为了给Vue一个提示，以便它能跟踪每个节点的身份，从而在保证有状态的列表被正确更新的前提下，提升渲染的性能。此时，需要为每项提供一个唯一的key属性。

![image-20220422201022396](/assets/img/article/image-20220422201022396.png)

#### key的注意事项

① key的值只能是**字符串**或**数字**类型
② key的值**必须具有唯一性**（即：key的值不能重复）
③ 建议把**数据项id属性的值**作为key的值（因为id属性的值具有唯一性）
④ 使用**index的值**当作key的值**没有任何意义**（因为index的值不具有唯一性）
⑤ 建议使用v-for指令时**一定要指定key的值**（既提升性能、又防止列表状态紊乱）

## 2.过滤器

> vue3 移除了过滤器

过滤器(Filters)常用于文本的格式化。例如：
hello -> Hello

过滤器应该被添加在JavaScript表达式的尾部，由"管道符”进行调用，示例代码如下：

![image-20220422201704881](/assets/img/article/image-20220422201704881.png)

过滤器可以用在两个地方：插值表达式和v-bind属性绑定。

### 2.1定义过滤器

在创建vue实例期间，可以在filters节点中定义过滤器，示例代码如下：

![image-20220422201835717](/assets/img/article/image-20220422201835717.png)

### 2.2私有过滤器和全局过滤器

在filters节点下定义的过滤器，称为“私有过滤器”，因为它只能在当前vm实例所控制的el区域内使用。
如果希望在多个vue实例之间共享过滤器，则可以按照如下的格式定义全局过滤器：

![image-20220422202112190](/assets/img/article/image-20220422202112190.png)

就近原则

### 2.3连续调用多个过滤器

过滤器可以串联地进行调用，例如：

![image-20220422202444640](/assets/img/article/image-20220422202444640.png)

示例代码如下：

![image-20220422202523330](/assets/img/article/image-20220422202523330.png)

### 2.4过滤器传参

过滤器的本质是JavaScript函数，因此可以接收参数，格式如下：

![image-20220422202656996](/assets/img/article/image-20220422202656996.png)

示例代码如下：

![image-20220422202746776](/assets/img/article/image-20220422202746776.png)

### 2.5过滤器的兼容性

过滤器仅在vue2.X和1.X中受支持，在vue3.x的版本中剔除了过滤器相关的功能。

在企业级项目开发中：

- 如果使用的是2.×版本的Vue,则依然可以使用过滤器相关的功能

- 如果项目已经升级到了3.X版本的Vue,官方建议使用计算属性或方法代替被剔除的过滤器功能

具体的迁移指南，请参考Vue3.X的官方文档给出的说明：
https://v3.vuejs.org/guide/migration/filters.html#migration-strategy

# 品牌列表案例
