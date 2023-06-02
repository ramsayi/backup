---
title: VSCode报错Vetur can't find解决方法
tags:
  - VSCode
categories:
  - 踩坑记录
  - VSCode
cover: '/assets/img/post/vscode.webp'
abbrlink: 6ed96e7
date: 2022-04-28 19:08:26
---

![image-20220428190922443](/assets/img/article/image-20220428190922443.png)

**原因**

Vetur 0.31.0版本新增了一个vetur.config.js的配置文件，

在这个版本之后，会优先查找项目中是否配有tsconfig.json（ts项目）或者jsconfig.json（js项目），

没找到这2个文件就去找vetur.config.js，如果都没有，就会抛出这个提示。

**说明**

[VSCode](https://so.csdn.net/so/search?q=VSCode&spm=1001.2101.3001.7020)的JavaScript支持可以在两种不同的模式下运行：

**文件范围（没有jsconfig.json）**

在此模式下，在VSCode中打开的JavaScript文件被视为独立单元。

只要文件a.js没有显式引用文件b.ts（使用///引用指令或CommonJS模块），两个文件之间就没有共同的项目上下文。

**显式项目（使用jsconfig.json）**

JavaScript项目是通过jsconfig.json文件定义的。目录中存在此类文件表示该目录是JavaScript项目的根目录。

文件本身可以选择列出属于项目的文件，要从项目中排除的文件，以及编译器选项（见下文）。



当您在工作空间中有一个定义项目上下文的jsconfig.json文件时，JavaScript体验会得到改进。

因此，当您在新工作空间中打开JavaScript文件时，我们提供了一个创建jsconfig.json文件的提示。



**解决方法（3选1）**

1.配置Vetur插件，忽略提示：

```javascript
vetur.ignoreProjectWarning: true
```

2.在项目根目录创建jsconfig.json文件，加入代码：

```json
{
    "include": [
        "./src/*"
    ]
}
```

3.在项目根目录创建vetur.config.js文件，加入代码：

```ruby
module.exports = {
    // vetur配置，会覆盖vscode中的设置。  default: `{}`
    settings: {
        "vetur.useWorkspaceDependencies": true,
        "vetur.experimental.templateInterpolationService": true
    },
    // 普通项目采用默认配置 default: `[{ root: './' }]`
}
```
