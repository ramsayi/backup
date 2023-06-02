---
title: （一）前端工程化与webpack
tags:
  - Vue3
categories:
  - 技术学习
  - Vue
abbrlink: 87137f47
date: 2022-04-20 09:56:29
cover: /assets/img/post/webpack.webp
---

# 前端工程化

## 1.小白眼中的前端开发vs实际的前端开发

小白眼中的前端开发：

- 会写 HTML + CSS + JavaScript 就会前端开发
- 需要美化页面样式，就拽一个bootstrap过来
- 需要操作 DOM 或发起 Ajax 请求，再拽一个jQuery 过来
- 需要渲染模板结构，就用art-template等模板引擎

实际的前端开发：

- 模块化 (js 的模块化、css的模块化、其它资源的模块化）
- 组件化 (复用现有的UI结构、样式、行为）
- 规范化 (目录结构的划分、编码规范化、接口规范化、文档规范化、Git分支管理)
- 自动化（自动化构建、自动部署、自动化测试）

## 2. 什么是前端工程化
前端工程化指的是：在企业级的前端项目开发中，把前端开发所需的工具、技术、流程、经验等进行规范化、
标准化。最终落实到细节上，就是实现前端的“4 个现代化”：模块化、组件化、规范化、自动化

## 3.前端工程化的好处

前端工程化的好处主要体现在如下两方面：
① 前端工程化让前端开发能够“自成体系”，覆盖了前端项目从创建到部署的方方面面
② 最大程度地提高了前端的开发效率，降低了技术选型、前后端联调等带来的协调沟通成本

## 4.前端工程化的解决方案

早期的前端工程化解决方案：

- grunt ( https://www.gruntjs.net/ )
- gulp ( https://www.gulpjs.com.cn/ )

目前主流的前端工程化解决方案：

- webpack ( https://www.webpackjs.com/ )
- parcel ( https://zh.parceljs.org/ )

# webpack 的基本使用

## 1. 什么是 webpack

概念：webpack 是前端项目工程化的具体解决方案。

主要功能：它提供了友好的前端模块化开发支持，以及代码压缩混淆、处理浏览器端JavaScript的兼容性、性能优化等强大的功能。

好处：让程序员把工作的重心放到具体功能的实现上，提高了前端开发效率和项目的可维护性。
注意：目前企业级的前端项目开发中，绝大多数的项目都是基于webpack进行打包构建的。

## 2. 创建列表隔行变色项目
① 新建项目空白目录，并运行 `npm init -y` 命令，初始化包管理配置文件 `package.json`
② 新建 src 源代码目录
③ 新建 src -> index.html 首页和 src -> index.js 脚本文件
④ 初始化首页基本的结构
⑤ 运行 npm install jquery -S 命令，安装 jQuery
⑥ 通过 ES6 模块化的方式导入 jQuery，实现列表隔行变色效果

## 3.在项目中安装 webpack

在终端运行如下的命令，安装webpack相关的两个包：
`npm install webpack@5.5.1 webpack-cli@4.2.0 -D`

## 4.在项目中配置 webpack

① 在项目根目录中，创建名为 `webpack.config.js` 的 webpack 配置文件，并初始化如下的基本配置：

```js
module.exports = {
    mode: 'development' // mode 用来指定构建模式。可选值有 development 和 production
}
```

② 在 package.json 的 scripts 节点下，新增 `dev 脚本` 如下：

```json
"scripts": {
  "dev": "webpack" // script 节点下的脚本，可以通过 npm run 执行。例如 npm run dev
},
```

③ 在终端中运行 `npm run dev` 命令，启动 webpack 进行项目的打包构建

### 4.1 mode的可选值

mode 节点的可选值有两个，分别是：
① development

- 开发环境
- 不会对打包生成的文件进行代码压缩和性能优化
- 打包速度快，适合在开发阶段使用

② production

- 生产环境
- 会对打包生成的文件进行代码压缩和性能优化
- 打包速度很慢，仅适合在项目发布阶段使用

### 4.2 webpack.config.js文件的作用

webpack.config.js 是 webpack 的配置文件。webpack 在真正开始打包构建之前，会先读取这个配置文件，从而基于给定的配置，对项目进行打包。
注意：由于 webpack 是基于 node.js 开发出来的打包工具，因此在它的配置文件中，支持使用 node.js 相关的语法和模块进行 webpack 的个性化配置。

### 4.3 webpack中的默认约定

在 webpack 中有如下的默认约定：
① 默认的打包入口文件为 src -> index.js
② 默认的输出文件路径为 dist -> main.js

注意：可以在 webpack.config.js 中修改打包的默认约定

### 4.4 自定义打包的入口与出口

在 webpack.config.js 配置文件中，通过 entry 节点指定打包的入口。通过 output 节点指定打包的出口。
示例代码如下：

```js
const path = require('path') // 导入 node.js 中专门操作路径的模块

module.exports = {
    entry: path.join(__dirname, './src/index.js'), // 打包入口文件的路径
    output: {
        path: path.join(__dirname, './dist'), // 输出文件的存放路径
        filename: 'bundle.js' //输出文件的名称
    }
}
```

# webpack 中的插件

## 1. webpack 插件的作用
通过安装和配置第三方的插件，可以拓展 webpack 的能力，从而让 webpack 用起来更方便。最常用的 webpack 插件有如下两个：

① webpack-dev-server

- 类似于 node.js 阶段用到的 nodemon 工具
- 每当修改了源代码，webpack 会自动进行项目的打包和构建

② html-webpack-plugin

- webpack 中的 HTML 插件（类似于一个模板引擎插件）
- 可以通过此插件自定制 index.html 页面的内容

## 2. webpack-dev-server
webpack-dev-server可以让webpack监听项目源代码的变化，从而进行自动打包构建。

### 2.1 安装 webpack-dev-server

运行如下的命令，即可在项目中安装此插件：

`npm install webpack-dev-server@3.11.0 -D`

### 2.2 配置 webpack-dev-server

① 修改 package.json -> scripts 中的 dev 命令如下：

```json
"scripts": {
    "dev": "webpack serve", // script 节点下的脚本，可以通过 npm run 执行。例如 npm run dev
}
```

② 再次运行 npm run dev 命令，重新进行项目的打包

③ 在浏览器中访问 http://localhost:8080 地址，查看自动打包效果

### 2.3 打包生成的文件哪儿去了？

① 不配置 webpack-dev-server的情况下,webpack打包生成的文件，会存放到实际的物理磁盘上

- 严格遵守开发者在 webpack.config.js 中指定配置
- 根据 output 节点指定路径进行存放

② 配置了webpack-dev-server之后，打包生成的文件存放到了内存中

- 不再根据output节点指定的路径，存放到实际的物理磁盘上
- 提高了实时打包输出的性能，因为内存比物理磁盘速度快很多

### 2.4生成到内存中的文件该如何访问？

webpack-dev-server生成到内存中的文件，默认放到了项目的根目录中，而且是虚拟的、不可见的。

## 3.html-webpack-plugin

html-webpack-plugin是webpack中的HTML插件，可以通过此插件自定制index.html页面的内容。
需求：通过html-webpack-plugin插件，将src目录下的index.html首页，复制到项目根目录中一份！

### 3.1安装html-webpack-plugin

运行如下的命令，即可在项目中安装此插件：

`npm install html-webpack-plugin@4.5.0 -D`

### 3.2配置html-webpack-plugin

```js
// 1. 导入 HTML 插件，得到一个构造函数
const HtmlPlugin = require('html-webpack-plugin')

// 2. 创建 HTML 插件的实例对象
const htmlPlugin = new HtmlPlugin({
    template: './src/index.html', // 指定原文件的存放路径
    filename: './index.html', // 指定生成的文件的存放路径
})

module.exports = {
    mode: 'development',
    plugins: [htmlPlugin], // 通过 plugin 节点，使 htmlPlugin 插件生效
}
```

### 3.3解惑html-webpack-plugin

① 通过HTML插件复制到项目根目录中的index.html页面，也被放到了内存中
② HTML插件在生成的index.html页面的底部，自动注入了打包的bundle.js文件

## 4.devServer节点

在webpack.config,js配置文件中，可以通过devServer节点对webpack-dev-server插件进行更多的配置，
示例代码如下：

```js
devServer: {
	open: true, // 初次打包完成后，自动打开浏览器
	host: '127.0.0.1', // 实时打包所使用的主机地址
	port: 80, // 实时打包所使用的端口号
}
```

# webpack 中的 loader

## 1.loader概述

在实际开发过程中，webpack默认只能打包处理以.js后缀名结尾的模块。其他非.js后缀名结尾的模块，webpack默认处理不了，需要调用loader加载器才可以正常打包，否则会报错！

loader加载器的作用：协助webpack打包处理特定的文件模块。比如：

- css-loader可以打包处理.css相关的文件
- less-loader可以打包处理.less相关的文件
- babel-loader可以打包处理webpack无法处理的高级JS语法

## 2.loader的调用过程

![image-20220420224028670](/assets/img/article/image-20220420224028670.png)

## 3.打包处理css文件

①运行`npm i style-loader@2.0.0 css-loader@5.0.1-D`命令，安装处理css文件的loader

②在webpack.config.js的module->rules数组中，添加loader规则如下：

```js
module: { // 所有第三方文件模块的匹配规则
    rules: [ // 文件后缀名的匹配规则
        { test: /\.css$/, use: ['style-loader', 'css-loader'] }
    ]
}
```

其中，test表示匹配的文件类型，use表示对应要调用的loader

注意：
use数组中指定的loader顺序是固定的
多个loader的调用顺序是：从后往前调用

## 4.打包处理less文件

①运行`npm i less-loader@7.1.0 less@3.12.2 -D`命令
②在webpack.config.js的module->rules数组中，添加loader规则如下：

```js
module: { // 所有第三方文件模块的匹配规则
    rules: [ // 文件后缀名的匹配规则
        { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
    ]
}
```

## 5.打包处理样式表中与ul路径相关的文件

> webpack 5 此项失效

①运行`npm i url-loader@4.1.1 file-loader@6.2.0 -D`命令
②在webpack..config.js的module->rules数组中，添加loader规则如下：

```js
module: { // 所有第三方文件模块的匹配规则
    rules: [ // 文件后缀名的匹配规则
        { test: /\.jpg|png|gifs/, use: 'url-loader?limit=22229' },
    ]
}
```

其中？之后的是loader的参数项：
limit用来指定图片的大小，单位是字节(byte)
只有≤limit大小的图片，才会被转为base64格式的图片

### 5.1 loader的另一种配置方式

带参数项的loader还可以通过对象的方式进行配置：

```js
module: { // 所有第三方文件模块的匹配规则
    rules: [ // 文件后缀名的匹配规则
        {
            test: /\.jpg|png|gif$/,  // 匹配图片文件
         	use: {
                loader: 'url-loader', // 通过 loader 属性指定要调用的 loader
                options: { // 通过 optiions 属性指定参数项
                    limit: 22229
                }
            }
        }
    ]
}
```

## 6.打包处理js文件中的高级语法

webpack只能打包处理一部分高级JavaScript语法。对于那些webpack无法处理的高级js语法，需要借助于babel-loader进行打包处理。例如webpack无法处理下面的JavaScript代码：

```js
class Person {
    //通过static关键字，为Person类定义了一个静态属性info
	//webpack无法打包处理"静态属性"这个高级语法
    static info = 'person info'
}

console.log(Person.info)
```

### 6.1安装babel-loader相关的包

运行如下的命令安装对应的依赖包：

```bash
npm i babel-loader@8.2.1 @babel/core@7.12.3 @babel/plugin-proposal-class-properties@7.12.1 -D  
```

包的名称及版本号列表如下（红色是包的名称、黑色是包的版本号）：

- @babel-loader@8.2.1
- @babel/core@7.12.3
- @babel/plugin-proposal-class-properties@7.12.1

### 6.2配置babel-loader

在webpack.config.js的module->rules数组中，添加loader规则如下：

```js
{
	test: /\.js$/,
	//exclude为排除项，
	//表示babel-loader只需处理开发者编写的js文件，不需要处理node_modules下的js文件
	exclude: /node_modules/,
	use: {
		loader:'babel-loader',
		options:{ //参数项
			//声明一个babel插件，此插件用来转化class中的高级语法
			plugins:['@babel/plugin-proposal-class-properties'],
		},
	},
}
```

# 打包发布

## 1.为什么要打包发布

项目开发完成之后，使用webpack对项目进行打包发布的主要原因有以下两点：

①开发环境下，打包生成的文件存放于内存中，无法获取到最终打包生成的文件
②开发环境下，打包生成的文件不会进行代码压缩和性能优化

为了让项目能够在生产环境中高性能的运行，因此需要对项自进行打包发布。

## 2.配置webpack的打包发布

在package.json文件的scripts节点下，新增build命令如下：

```json
"scripts": {
    "dev": "webpack serve", // 开发环境中，运行dev命令
    "build": "webpack --mode production" // 项目发布时，运行build命令
}
```

`--model`是一个参数项，用来指定webpack的运行模式。production代表生产环境，会对打包生成的文件进行代码压缩和性能优化。

注意：通过--model指定的参数项，会覆盖webpack.config.js中的model选项。

## 3.把JavaScript文件统一生成到js目录中

在 webpack.config.js 配置文件的 output 节点中，进行如下的配置：

```js
output: {
	path: path.join(__dirname, 'dist'),
	// 明确告诉webpack把生成的bundle.js文件存放到dist目录下的js子目录中
	filename: 'js/bundle.js',
}
```

## 4.把图片文件统一生成到 image 目录中

修改webpack.config.js中的url-loader配置项，新增outputPath选项即可指定图片文件的输出路径：

```js
{
	test: /\.jpg|png|gif$/,
    use: {
        loader: 'url-loader',
        options: {
            limit: 22228,
            //明确指定把打包生成的图片文件，存储到dist目录下的image文件夹中
            outputPath: 'image',
        }
    }
}
```

## 5.自动清理dist目录下的旧文件

为了在每次打包发布时自动清理掉dist目录中的旧文件，可以安装并配置`clean-webpack-plugin`插件：

```js
//1.安装清理dist目录的webpack插件
npm install clean-webpack-plugin@3.0.0 -D

//2.按需导入插件、得到插件的构造函数之后，创建插件的实例对象
const { CleanWebpackPlugin } = require('clean-webpack-plugin')
const cleanPlugin = new CleanWebpackPlugin()

//3.把创建的cleanPlugin插件实例对象，挂载到plugins节点中
plugins: [htmlPlugin, cleanPlugin], //挂载插件
```

## 6.企业级项目的打包发布

企业级的项目在进行打包发布时，远比刚才的方式要复杂的多，主要的发布流程如下：
● 生成打包报告，根据报告分析具体的优化方案
● Tree-Shaking
● 为第三方库启用CDN加载
● 配置组件的按需加载
● 开启路由懒加载
● 自定制首页内容
在后面的Vue项目课程中，会专门讲解如何进行企业级项目的打包发布。

# Source Map

## 1.生产环境遇到的问题

前端项目在投入生产环境之前，都需要对JavaScript源代码进行压缩混淆，从而减小文件的体积，提高文件的加载效率。此时就不可避免的产生了另一个问题：
对压缩混淆之后的代码除错(debug)是一件极其困难的事

![image-20220421194606481](/assets/img/article/image-20220421194606481.png)

变量被替换成没有任何语义的名称
空行和注释被剔除

## 2.什么是Source Map

Source Map就是一个信息文件，里面储存着位置信息。也就是说，Source Map文件中存储着代码压缩混淆前后的对应关系。
有了它，出错的时候，除错工具将直接显示原始代码，而不是转换后的代码，能够极大的方便后期的调试。

## 3.webpack开发环境下的Source Map

在开发环境下，webpack默认启用了Source Map功能。当程序运行出错时，可以直接在控制台提示错误行的位置，并定位到具体的源代码：

![image-20220421194722191](/assets/img/article/image-20220421194722191.png)

### 3.1默认Source Map的问题

开发环境下默认生成的Source Map,记录的是生成后的代码的位置。会导致运行时报错的行数与源代码的行数不一致的问题。示意图如下：
![image-20220421194801281](/assets/img/article/image-20220421194801281.png)

### 3.2解决默认Source Map的问题

开发环境下，推荐在webpack.config.js中添加如下的配置，即可保证运行时报错的行数与源代码的行数保持一致：

```js
module.exports = {
	mode: 'development',
    //eval-source-map仅限在"开发模式"下使用，不建议在"生产模式"下使用。
	//此选项生成的Source Map能够保证"运行时报错的行数"与"源代码的行数"保持一致
    devtool: 'eval-source-map',
}
```

## 4.webpack生产环境下的Source Map

在生产环境下，如果省略了devtool选项，则最终生成的文件中不包含Source Map。这能够防止原始代码通过Source Map的形式暴露给别有所图之人。

![image-20220421195301188](/assets/img/article/image-20220421195301188.png)

### 4.1只定位行数不暴露源码

在生产环境下，如果只想定位报错的具体行数，且不想暴露源码。此时可以将devtool的值设置为
`nosources-source-map`。实际效果如图所示：

![image-20220421195459183](/assets/img/article/image-20220421195459183.png)

### 4.2定位行数且暴露源码

在生产环境下，如果想在定位报错行数的同时，展示具体报错的源码。此时可以将devtool的值设置为`source-map`。实际效果如图所示：

![image-20220421195547496](/assets/img/article/image-20220421195547496.png)

采用此选项后：你应该将你的服务器配置为，不允许普通用户访问source map文件！

## 5.Source Map的最佳实践

①开发环境下：

- 建议把devtool的值设置为eval-source-map
- 好处：可以精准定位到具体的错误行

②生产环境下：

- 建议关闭Source Map或将devtool的值设置为nosources-source-map
- 好处：防止源码泄露，提高网站的安全性

![image-20220421195745692](/assets/img/article/image-20220421195745692.png)
