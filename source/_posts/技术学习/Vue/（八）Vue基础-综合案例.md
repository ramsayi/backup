---
title: （八）Vue基础-综合案例
tags:
  - Vue3
categories:
  - 技术学习
  - Vue
cover: '/assets/img/post/vuejs.webp'
abbrlink: d7f18edd
date: 2022-05-04 20:53:40
---

# vue-cli

## 1.什么是vue-cli

vue-cli（俗称: vue脚手架）是vue官方提供的、快速生成vue工程化项目的工具。

特点:

1. 开箱即用
2. 基于webpack
3. 功能丰富且易于扩展
4. 支持创建vue2和vue3的项目

vue-cli的中文官网首页: https://cli.vuejs.org/zh/

## 2.安装vue-cli

vue-cli是基于Node.js 开发出来的工具，因此需要使用npm将它安装为全局可用的工具:

```bash
# 全局安装 vue-cli
npm install -g @vue/cli

# 查看 vue-cli 的版本，检验 vue-cli 是否安装成功
vue --version
```

### 2.1解决Windows PowerShell 不识别vue命令的问题

默认情况下，在PowerShell中执行`vue --version`命令会提示如下的错误消息:

![image-20220504205943998](/assets/img/article/image-20220504205943998.png)

解决方案如下︰

1. 以管理员身份运行PowerShell

2. 执行`set-ExecutionPolicy RemoteSigned`命令
3. 输入字符`Y`，回车即可

![image-20220504210048019](/assets/img/article/image-20220504210048019.png)

## 3.创建项目

vue-cli提供了创建项目的两种方式:

```bash
# 基于【命令行】的方式创建 vue 项目
vue create 项目名称

# OR

# 基于【可视化面板】创建 vue 项目
vue ui
```

## 4.基于vue ui创建vue项目

步骤1:在终端下运行`vue ui`命令，自动在浏览器中打开创建项目的可视化面板:

![image-20220504211624484](/assets/img/article/image-20220504211624484.png)

步骤2:在详情页面填写项目名称:

![image-20220504211651730](/assets/img/article/image-20220504211651730.png)

步骤3:在预设页面选择手动配置项目:

![image-20220504212112372](/assets/img/article/image-20220504212112372.png)

步骤4∶在功能页面勾选需要安装的功能（Choose Vue Version、Babel、CSS预处理器、使用配置文件):

![image-20220504212207626](/assets/img/article/image-20220504212207626.png)

步骤5:在配置页面勾选vue的版本和需要的预处理器:

![image-20220504212258691](/assets/img/article/image-20220504212258691.png)

步骤6∶将刚才所有的配置保存为预设（模板），方便下一次创建项目时直接复用之前的配置:

![image-20220504212325721](/assets/img/article/image-20220504212325721.png)

vue ui的本质:通过可视化的面板采集到用户的配置信息后，在后台基于命令行的方式自动初始化项目

项目创建完成后，自动进入项目仪表盘:

![image-20220504212450010](/assets/img/article/image-20220504212450010.png)

## 5.基于命令行创建vue项目

步骤1:在终端下运行`vue create demo2`命令，基于交互式的命令行创建vue的项目:

![image-20220504212929926](/assets/img/article/image-20220504212929926.png)

步骤2:选择要安装的功能:

![image-20220504212957441](/assets/img/article/image-20220504212957441.png)

步骤3:使用上下箭头选择vue的版本，并使用回车键确认选择

![image-20220504213056688](/assets/img/article/image-20220504213056688.png)

步骤4:使用上下箭头选择要使用的css 预处理器，并使用回车键确认选择:

![image-20220504213126100](/assets/img/article/image-20220504213126100.png)

步骤5:使用上下箭头选择如何存储插件的配置信息，并使用回车键确认选择:

![image-20220504213149297](/assets/img/article/image-20220504213149297.png)

步骤6:是否将刚才的配置保存为预设:

![image-20220504213217453](/assets/img/article/image-20220504213217453.png)

步骤7:选择如何安装项目中的依赖包:

![image-20220504213244139](/assets/img/article/image-20220504213244139.png)

## 6.梳理vue2项目的基本结构

![image-20220504213400885](/assets/img/article/image-20220504213400885.png)

主要的文件:
src -> App.vue
src ->main.js

## 7.分析main.js中的主要代码

```js
// 1.导入 Vue 的构造函数
import Vue from 'vue'
// 2.导入 App 根组件
import App from './App.vue'

// 屏蔽浏览器 console 面板的提示信息
Vue.config.productionTip = false

// 3.创建 vue 实例对象
new Vue({
    render: h => h(App), // 3,1 使用 render 函数渲染 App 根组件
}).$mount('#app')        // 3.2 把 App 根组件渲染到 $mount 函数指定的 el 区域中
```

## 8.在vue2的项目中使用路由

在vue2的项目中，只能安装并使用3.x版本的vue-router。
版本3和版本4的路由最主要的区别: 创建路由模块的方式不同!.

### 8.1回顾:4.x版本的路由如何创建路由模块

```js
import { createRouter, creatWebHashHistory } from 'vue-router' // 1.按需导入需要的方法

import MyHome from './Home.vue'              // 2.导入需要使用的路由进行切换的组件
import MyMovie from './Movie.vue'

const router = createRouter({                // 3.创建路由对象
    history: createWebHashHistory(),         // 3.1 指定通过 hash 管理路由的切换
    routes: [                                // 3.2 创建路由规则
        { path: '/home', component: MyHome },
        { path: '/movie', component: MyMovie },
    ]
})

export default router                        // 4.向外共享路由对象
```

### 8.2学习:3.x版本的路由如何创建路由模块

步骤1:在vue2的项目中安装3.x版本的路由:

```bash
npm i vue-router@3.4.9 -S
```

步骤2:在src -> components目录下，创建需要使用路由切换的组件:

![image-20220504220221714](/assets/img/article/image-20220504220221714.png)

步骤3:在src目录下创建router -> index.js路由模块:

```js
import Vue from 'vue'                      // 1. 导入 Vue2 的构造函数
import VueRouter from 'vue-router'         // 2. 导入 3.x 路由的构造函数

import Home from '@/components/Home.vue'   // 3. 导入需要使用路由切换的组件
import Movie from '@/components/Movie.vue'

Vue.use(VueRouter)                         // 4. 调用 Vue.use() 函数，把路由配置为 Vue 的插件

const router = new VueRouter({             // 5. 创建路由对象
    routes: [                              // 5.1 声明路由规则
        { path: '/', redirect: 'home' },
        { path; '/home', component: Home },
        { path: '/movie', component: Movie },
    ]
})

export default router                      // 6.向外共享路由对象
```

步骤4:在main.js 中导入路由模块，并通过router属性进行挂载:

```js
import Vue from 'vue'
import App from './App.vue'
// 1. 导入路由模块
import router from './router'

Vue.config.productionTip = false

new Vue({
    render: h => h(App),
    // 2. 挂载路由模块
    // router: router,
    router,
}).$mount('#app')
```

步骤5:在App.vue根组件中，使用`<router-view>`声明路由的占位符:

```vue
<template>
	<div>
        <h1>App 根组件</h1>
        <hr />
        <!-- 声明路由的占位符 -->
        <router-view></router-view>
    </div>
</template>
```

# 组件库

## 1.什么是vue组件库

在实际开发中，前端开发者可以把自己封装的.vue组件整理、打包、并发布为npm 的包，从而供其他人下载和使用。这种可以直接下载并在项目中使用的现成组件，就叫做vue组件库。

## 2. vue组件库和bootstrap的区别
二者之间存在本质的区别:

- bootstrap只提供了纯粹的原材料（css样式、HTML结构以及 JS特效)，需要由开发者做进一步的组装和改造
- vue组件库是遵循vue语法、高度定制的现成组件，开箱即用

## 3.最常用的vue组件库

PC端：Element UI、View ul

移动端：Mint Ul、Vant

## 4.Element UI

Element UI是饿了么前端团队开源的一套PC端vue组件库。支持在八ue2和vue3的项目中使用:

- vue2的项目使用旧版的Element UI
- vue3的项目使用新版的Element Plus

### 4.2在vue2的项目中安装element-ui

运行如下的终端命令:

```bash
npm i element-ui -S
```

### 4.2引入element-ui

开发者可以一次性完整引入所有的element-ui组件，或是根据需求，只按需引入用到的element-ui组件:

- 完整引入︰操作简单，但是会额外引入一些用不到的组件，导致项目体积过大
- 按需引入︰操作相对复杂一些，但是只会引入用到的组件, 能起到优化项目体积的目的

### 4.3完整引入

在main.js 中写入以下内容:

```js
import Vue from 'vue'
import App from './App.vue'
// 1. 完整引入 element-ui 的组件
import ElementUI from 'element-ui'
// 2. 导入 element ui 组件的样式
import 'element-ui/lib/theme-chalk/index.css'

// 3. 把 ElementUI 注册为 Vue 的插件
Vue.use(ElementUI)

new Vue({
    render: h => h(App),
}).$mount('#app')
```

### 4.4按需引入

借助babel-plugin-component，我们可以只引入需要的组件，以达到减小项目体积的目的。

步骤1，安装babel-plugin-component:

```bash
npm i babel-plugin-component -D
```

步骤2，修改根目录下的babel.config.js配置文件，新增plugins节点如下:

```js
module.exports = {
	presets: ['@vue/cli-plugin-babel/preset'],
    plugins: [
        [
            'component',
            {
                libraryName: 'element-ui',
                styleLibraryName: 'theme-chalk',
            },
        ],
    ],
}
```

步骤3，如果你只希望引入部分组件，比如Button，那么需要在main.js 中写入以下内容:

```js
import Vue from 'vue'
import App from './App.vue'
// 1. 导入 element ui 的组件
import { Button } from 'element-ui'

// 2. 注册需要的组件
Vue.component(Button.name, Button)
/* 或写为
 * Vue.use(Button)
 */

new Vue({
    render: h => h(App),
}).$mount('#app')
```

### 4.5把组件的导入和注册封装为独立的模块

在src目录下新建element-ui/index.js模块，并声明如下的代码:

```js
// 模块路径 /src/element-ui/index.js
import Vue from 'vue'
// 按需导入 element ui 的组件
import { Button, Input } from 'element-ui'

// 注册需要的组件
Vue.use(Button)
Vue.use(Input)

// 在 main.js 中导入
import './element-ui'
```

# axios拦截器

## 1.回顾:在vue3的项目中全局配置axios

```js
import { createApp } from 'vue'
import App from './App.vue'
// 1. 导入 axios
import axios from 'axios'

const app = creatApp(App)
// 2. 配置请求根路径
axios.default.baseURL = 'https://www.escook.cn'
// 3. 全局配置 axios
app.config.globalProperties.$http = axios
app.mount('#app')
```

## 2.在vue2的项目中全局配置axios

需要在main.js入口文件中，通过Vue构造函数的prototype原型对象全局配置axios:

```js
import Vue from 'vue'
import App from './App.vue'
// 1. 导入 axios
import axios from 'axios'

// 2. 配置请求根路径
axios.defaults.baseURL = 'https://www.escook.cn'
// 3. 通过 Vue 构造函数的原型对象，全局配置 axios
Vue.prototype.$http = axios

new Vue({
    render: h => h(App),
}).$mount('#app')
```

## 3.什么是拦截器

拦截器（英文:Interceptors）会在每次发起ajax请求和得到响应的时候自动被触发。

![image-20220505150028876](/assets/img/article/image-20220505150028876.png)

应用场景:

- Token身份认证

- Loading效果
- etc...

## 4.配置请求拦截器

通过axios.interceptors.request.use(成功的回调,失败的回调)可以配置请求拦截器。示例代码如下:

```js
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });
```

注意：失败的回调函数可以被省略！

### 4.1 请求拦截器 – Token 认证

```js
import axios from 'axios'

axios.defaults.baseURL = 'https://www.escook.cn'
// 配置请求的拦截器
axios.interceptors.request.use(config => {
    // 为当前请求配置 Token 认证字段
    config.headers.Authorization = 'Bearer xxx'
    return config
})

Vue.prototype.$http = axios
```

### 4.2 请求拦截器 – 展示 Loading 效果 

借助于 element ui 提供的 Loading 效果组件（https://element.eleme.cn/#/zh-CN/component/loading） 可以方便的实现 Loading 效果的展示：

```js
// 1. 按需导入 Loading 效果组件
import { Loading } from 'element-ui'

// 2. 声明变量，用来存储 Loading 组件的实例对象
let loadingInstance = null

// 配置请求的拦截器
axios.interceptors.request.use(config => {
    // 3. 调用 Loading 组件的 service() 方法，创建 Loading 组件的实例，并全屏展示 loading 效果
    loadingInstance = Loading.service({ fullscreen: true })
    return config
})
```

## 5.配置响应拦截器

通过`axios.interceptors.response.use(成功的回调,失败的回调)`可以配置响应拦截器。示例代码如下:

```js
// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 2xx 范围内的状态码都会触发该函数。
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 超出 2xx 范围的状态码都会触发该函数。
    // 对响应错误做点什么
    return Promise.reject(error);
  });
```

注意：失败的回调函数可以被省略！

### 5.1 响应拦截器 – 关闭 Loading 效果

调用 Loading 实例提供的 close() 方法即可关闭 Loading 效果，示例代码如下：

```js
// 响应拦截器
axios.interceptors.response.use(response => {
    // 调用 Loading 实例的 close 方法即可关闭 loading 效果
    loadingInstance.close()
    return response;
  });
```

# proxy跨域代理

## 1.回顾:接口的跨域问题

vue项目运行的地址: http://localhost:8080/
API接口运行的地址: https://www.escook.cn/api/users

由于当前的API接口没有开启CORS跨域资源共享，因此默认情况下，上面的接口无法请求成功!

![image-20220505153307831](/assets/img/article/image-20220505153307831.png)

## 2. 通过代理解决接口的跨域问题

通过 vue-cli 创建的项目在遇到接口跨域问题时，可以通过代理的方式来解决：

![image-20220505153428237](/assets/img/article/image-20220505153428237.png)

① 把 axios 的请求根路径设置为 vue 项目的运行地址（接口请求不再跨域）
② vue 项目发现请求的接口不存在，把请求转交给 proxy 代理 
③ 代理把请求根路径替换为 devServer.proxy 属性的值，发起真正的数据请求 
④ 代理把请求到的数据，转发给 axios

## 3. 在项目中配置 proxy 代理

步骤1，在 main.js 入口文件中，把 axios 的请求根路径改造为当前 web 项目的根路径：

```js
// axios.defaults.baseURL = 'https://www.escook.cn'
// 配置请求根路径
axios.defaults.baseURL = 'http://localhost:8080'
```

步骤2，在项目根目录下创建 vue.config.js 的配置文件，并声明如下的配置：

```js
module.exports = {
    devServer: {
        // 当前项目在开发调试阶段，
        // 会将任何未知请求（没有匹配到静态文件的请求）代理到 https://www.escook.cn
        proxy: 'https://www.escook.cn'
    }
}
```

注意： 
① devServer.proxy 提供的代理功能，仅在开发调试阶段生效 
② 项目上线发布时，依旧需要 API 接口服务器开启 CORS 跨域资源共享

# 用户列表案例

略
