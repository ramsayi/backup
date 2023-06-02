---
title: （九）Vue全家桶-Vuex
tags:
  - Vue3
categories:
  - 技术学习
  - Vue
cover: '/assets/img/post/vuex.webp'
abbrlink: a7d23c1
date: 2022-05-04 19:45:58
---

# vuex概述

## 1.1组件之间共享数据的方式

父向子传值: v-bind属性绑定

子向受传值: v-on事件绑定

兄弟组件之间共享数据: EventBus

- `$on` 接收数据的那个组件
- `$emit` 发送数据的那个组件

## 1.2 Vuex是什么

Vuex是实现组件全局状态（数据）管理的一种机制，可以方便的实现组件之间数据的共享。

![image-20220506184253264](/assets/img/article/image-20220506184253264.png)

## 1.3使用Vuex统一管理状态的好处

1. 能够在vuex中集中管理共享的数据，易于开发和后期维护

2. 能够高效地实现组件之间的数据共享，提高开发效率
3. 存储在vuex中的数据都是响应式的，能够实时保持数据与页面的同步

## 1.4什么样的数据适合存储到Vuex中

一般情况下，只有组件之间共享的数据，才有必要存储到vuex中;

对于组件中的私有数据，依旧存储在组件自身的data中即可。

# Vuex的基本使用

## 1. 安装 vuex 依赖包

```bash
npm install vuex --save
```

## 2. 导入 vuex 包

```js
import Vuex from 'vuex'
Vue.use(Vuex)
```

## 3. 创建 store 对象

```js
const store = new Vuex.Store({
	// state 中存放的就是全局共享的数据
	state: { count: 0 }
})
```

## 4.将store对象挂载到vue实例中

```js
new vue ({
	el: '#app',
	render: h => h(app),
    router,
	//将创建的共享数据对象，挂载到 vue 实例中
	//所有的组件，就可以直接从 store 中获取全局的数据了
    store
})
```

# vuex的核心概念

## 1. 核心概念概述

vuex中的主要核心概念如下:

- State
- Mutation
- Action
- Getter

## 2. State

State提供唯一的公共数据源，所有共享的数据都要统一放到Store的 State中进行存储。

```js
// 创建store数据源，提供唯一公共数据
const store = new Vuex.Store({
    state: { count: 0 }
})
```

组件访问State中数据的第一种方式：

```js
this.$store.state.全局数据名称
```

组件访问State中数据的第二种方式：

```js
// 1. 从 vuex 中按需导入 mapState 函数
import { mapState } from 'vuex'
```

通过刚才导入的mapState函数，将当前组件需要的全局数据，映射为当前组件的computed计算属性

`...`是展开运算符，可以将全局数据映射为当前组件的计算属性

```js
// 2. 将全局数据，映射为当前组件的计算属性
computed: {
    ...mapState(['count'])
}
```

## 3. Mutation

Mutation用于变更Store中的数据。

1. 只能通过mutation变更Store 数据，不可以直接操作Store 中的数据。

2. 通过这种方式虽然操作起来稍微繁琐一些，但是可以集中监控所有数据的变化。

```js
// 定义 Mutation
const store = new Vuex.Store({
    state: {
        count: 0
    },
    mutations: {
        add(state) {
            // 变更状态
            state.count++
        }
    }
})
```

```js
// 触发mutation
methods: {
	handle1() {
		// 触发 mutations 的第一种方式
		this.$store.commit('add')
	}
}
```

可以在触发 mutations 时传递参数

```js
// 定义 Mutation
const store = new Vuex.Store({
    state: {
        count: 0
    },
    mutations: {
        addN(state, step) {
            // 变更状态
            state.count += step
        }
    }
})
```

```js
// 触发mutation
methods: {
	handle2() {
        // 在调用 commit 函数，
		// 触发 mutations 时携带参数
		this.$store.commit('addN', 3)
	}
}
```

this.$store.commit() 是触发 mutations 的第一种方式，触发 mutations 的第二种方式

```js
// 1. 从 vuex 中按需导入 mapMutations 函数
import { mapMutations } from 'vuex'
```

通过刚才导入的mapMutations函数，将需要的mutations函数，映射为当前组件的methods方法

```js
// 2. 将指定的 mutations 函数，映射为当前组件的 methods 函数
methods: {
	...mapMutations(['add','addN'])
}
```

## 4. Action

Action 用于处理异步任务

如果通过异步操作变更数据，必须通过 Action，而不能使用 Mutation，但是在 Action 中还是要通过触发 Mutation 的方式间接变更数据。

```js
// 定义 Action
const store = new Vuex.Store({
    // ...省略其他代码
    mutations: {
        add(state) {
            state.count++
        }
    },
    actions: {
    	addAsync(context) {
            setTimeout( () = > {
                context.commit('add')
            }, 1000)
        }
	}
})
```

```js
// 触发 Action
methods: {
    handle() {
        // 触发 actions 的第一种方式
        this.$store.dispatch('addAsync')
    }
}
```

触发 actions 异步任务时携带参数

```js
// 定义 Action
const store = new Vuex.Store({
	// ...省略其他代码
    mutations: {
        addN(state, step) {
            state.count += step
        }
    },
    actions: {
        addAsync(context, step) {
            setTimeout(() => {
                context.commit('addN', step)
            },1000)
        }
    }
})
```

```js
// 触发 Action
methods: {
    handle() {
        // 在调用 dispatch 函数，
        // 触发 actions 时携带参数
        this.$store.dispatch('addAsync', 5)
    }
}
```

this.$store.dispatch() 是触发 actions 的第一种方式，触发 actions 的第二种方式

```js
// 1. 从 vuex 中按需导入 mapActions 函数
import { mapActions } from 'vuex'
```

通过刚才导入的mapActions函数，将需要的actions函数，映射为当前组件的methods方法

```js
// 2. 将指定的 actions 函数，映射为当前组件的 methods 函数
methods: {
	...mapActions(['addASync','addNASync'])
}
```

## 5. Getter

Getter 用于对Store 中的数据进行加工处理形成新的数据。

1. Getter可以对Store 中已有的数据加工处理之后形成新的数据，类似Vue的计算属性。

2. Store中数据发生变化，Getter的数据也会跟着变化。

```js
// 定义 Getter
const store = new Vuex.Store({
	state: {
        count: 0
    },
    getters: {
        showNum: state => {
            return '当前最新的数量是【' + state.count + '】'
        }
    }
})
```

使用getters的第一种方式:

```js
this.$store.getters.名称
```

使用getters的第二种方式:

```js
import { mapGetters } from 'vuex'

computed: {
	...mapGetters(['showNum'])
}
```

# 基于Vuex的案例
