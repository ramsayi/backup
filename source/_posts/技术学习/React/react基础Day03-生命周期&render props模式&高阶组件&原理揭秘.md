---
title: react基础Day03-生命周期&render props模式&高阶组件&原理揭秘
tags:
  - React
categories:
  - 技术学习
  - React
cover: '/assets/img/post/react.webp'
abbrlink: 61aec8f
date: 2022-07-23 16:45:00
---

# 组件生命周期（★★★）

## 目标

- 说出组件生命周期对应的钩子函数
- 钩子函数调用的时机

## 概述

意义：组件的生命周期有助于理解组件的运行方式，完成更复杂的组件功能、分析组件错误原因等

组件的生命周期： 组件从被创建到挂载到页面中运行，再到组件不在时卸载的过程

生命周期的每个阶段总是伴随着一些方法调用，这些方法就是生命周期的钩子函数

构造函数的作用：为开发人员在不同阶段操作组件提供了实际

## 生命周期阶段

![](/assets/img/article/%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.png)

### 创建时（挂载阶段）

- 执行时机：组件创建时（页面加载时）
- 执行顺序

![](/assets/img/article/%E5%88%9B%E5%BB%BA%E6%97%B6-%E5%87%BD%E6%95%B0%E6%89%A7%E8%A1%8C%E9%A1%BA%E5%BA%8F.png)

![](/assets/img/article/%E5%88%9B%E5%BB%BA%E6%97%B6-%E5%87%BD%E6%95%B0%E7%9A%84%E4%BD%9C%E7%94%A8.png)

### 更新时

执行时机：`setState()、 forceUpdate()、 组件接收到新的props`

说明：以上三者任意一种变化，组件就会重新渲染

执行顺序：

![](/assets/img/article/%E6%9B%B4%E6%96%B0%E6%97%B6.png)

![](/assets/img/article/%E6%9B%B4%E6%96%B0%E6%97%B6-%E5%87%BD%E6%95%B0%E4%BD%9C%E7%94%A8.png)

### 卸载时

执行时机：组件从页面中消失

作用：用来做清理操作

![](/assets/img/article/%E5%8D%B8%E8%BD%BD%E6%97%B6.png)

### 不常用的钩子函数

#### 旧版的生命周期钩子函数

![](/assets/img/article/%E6%97%A7%E7%89%88%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%87%BD%E6%95%B0.png)

#### 新版完整生命会走棋钩子函数

![](/assets/img/article/%E6%96%B0%E7%89%88%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%87%BD%E6%95%B0.png)

##### `getDerivedStateFromProps()`

- **`getDerivedStateFromProps`** 会在调用 render 方法之前调用，并且在初始挂载及后续更新时都会被调用。它应返回一个对象来更新 state，如果返回 null 则不更新任何内容
- 不管原因是什么，都会在*每次*渲染前触发此方法

##### `shouldComponentUpdate()`

- 根据 **`shouldComponentUpdate()`** 的返回值，判断 React 组件的输出是否受当前 state 或 props 更改的影响。默认行为是 state 每次发生变化组件都会重新渲染
- 当 props 或 state 发生变化时，**`shouldComponentUpdate()`** 会在渲染执行之前被调用。返回值默认为 true

##### `getSnapshotBeforeUpdate()`

- **`getSnapshotBeforeUpdate()`** 在最近一次渲染输出（提交到 DOM 节点）之前调用。它使得组件能在发生更改之前从 DOM 中捕获一些信息（例如，滚动位置）。此生命周期的任何返回值将作为参数传递给 **`componentDidUpdate()`**
- 此用法并不常见，但它可能出现在 UI 处理中，如需要以特殊方式处理滚动位置的聊天线程等

# render-props模式 （★★★）

## 目标

- 知道render-props模式有什么作用
- 能够说出render-props的使用步骤

## React组件复用概述

- 思考：如果两个组件中的部分功能相似或相同，该如何处理？
- 处理方式：复用相似的功能
- 复用什么？
  - state
  - 操作state的方法
- 两种方式：
  - render props模式
  - 高阶组件（HOC）
- 注意： 这两种方式不是新的API，而是利用React自身特点的编码技巧，演化而成的固定模式

## 思路分析

- 思路：将要复用的state和操作state的方法封装到一个组件中

- 如何拿到该组件中复用的state

  - 在使用组件时，添加一个值为函数的prop，通过函数参数来获取

    ![](/assets/img/article/render-props-01.png)

- 如何渲染到任意的UI

  - 使用该函数的返回值作为要渲染的UI内容

    ![](/assets/img/article/render-props-02.png)

## 使用步骤

- 创建Mouse组件，在组件中提供复用的逻辑代码
- 将要复用的状态作为 props.render(state)方法的参数，暴露到组件外部
- 使用props.render() 的返回值作为要渲染的内容

![](/assets/img/article/render-props%E6%A8%A1%E5%BC%8F-01.png)

#### 示例demo

```react
class Mouse extends React.Component {
    // 鼠标位置状态
    state = {
        x: 0,
        y: 0
    }

    // 监听鼠标移动事件
    componentDidMount(){
        window.addEventListener('mousemove',this.handleMouseMove)
    }
    handleMouseMove = e => {
        this.setState({
            x: e.clientX,
            y: e.clientY
        })
    }
    render(){
        // 向外界提供当前子组件里面的数据
        return this.props.render(this.state)
    }
}
class App extends React.Component {
    render() {
        return (
            <div>
                App
                <Mouse render={mouse => {
                    return <p>X{mouse.x}Y{mouse.y}</p>
                }}/>
            </div>
        )
    }
}
ReactDOM.render(<App />,document.getElementById('root'))
```

## children代替render属性

- 注意：并不是该模式叫 render props就必须使用名为render的prop，实际上可以使用任意名称的prop
- 把prop是一个函数并且告诉组件要渲染什么内容的技术叫做： render props模式
- 推荐：使用childre代替render属性

![](/assets/img/article/render-props-children%E6%A8%A1%E5%BC%8F.png)

## 优化代码

- 推荐给render props模式添加props校验

![](/assets/img/article/%E4%BC%98%E5%8C%96-%E6%B7%BB%E5%8A%A0%E6%A0%A1%E9%AA%8C.png)

-  

![](/assets/img/article/%E4%BC%98%E5%8C%96-%E7%A7%BB%E9%99%A4%E4%BA%8B%E4%BB%B6%E7%BB%91%E5%AE%9A.png)



# 高阶组件 （★★★）

## 目标

- 知道高阶组件的作用
- 能够说出高阶的使用步骤

## 概述

- 目的：实现状态逻辑复用
- 采用 包装模式
- 手机：获取保护功能
- 手机壳：提供保护功能
- 高阶组件就相当于手机壳，通过包装组件，增强组件功能

![](/assets/img/article/%E6%89%8B%E6%9C%BA%E5%A3%B3.png)

## 思路分析

- 高阶组件(HOC、Higher-Order Component) 是一个函数，接收要包装的组件，返回增强后的组件

![](/assets/img/article/%E9%AB%98%E9%98%B6%E7%BB%84%E4%BB%B6-%E5%87%BD%E6%95%B0.png)

- 高阶组件内部创建了一个类组件，在这个类组件中提供复用的状态逻辑代码，通过prop将复用的状态传递给被包装组件`WrappedComponent`

![](/assets/img/article/%E9%AB%98%E9%98%B6%E7%BB%84%E4%BB%B6-%E7%B1%BB%E7%BB%84%E4%BB%B6%E5%86%85%E9%83%A8%E5%AE%9E%E7%8E%B0.png)

## 使用步骤

- 创建一个函数，名称约定以with开头
- 指定函数参数，参数应该以大写字母开头
- 在函数内部创建一个类组件，提供复用的状态逻辑代码，并返回
- 在该组件中，渲染参数组件，同时将状态通过prop传递给参数组件
- 调用该高阶组件，传入要增强的组件，通过返回值拿到增强后的组件，并将其渲染到页面

**包装函数**

```react
// 定义一个函数，在函数内部创建一个相应类组件
function withMouse(WrappedComponent) {
    // 该组件提供复用状态逻辑
    class Mouse extends React.Component {
        state = {
            x: 0,
            y: 0
        }
        // 事件的处理函数
        handleMouseMove = (e) => {
            this.setState({
                x: e.clientX,
                y: e.clientY
            })
        }
        // 当组件挂载的时候进行事件绑定
        componentDidMount() {
            window.addEventListener('mousemove', this.handleMouseMove)
        }
        // 当组件移除时候解绑事件
        componentWillUnmount() {
            window.removeEventListener('mousemove', this.handleMouseMove)
        }
        render() {
            // 在render函数里面返回传递过来的组件，把当前组件的状态设置进去
            return <WrappedComponent {...this.state} />
        }
    }
    return Mouse
}
```

**哪个组件需要加强，通过调用`withMouse`这个函数，然后把返回的值设置到父组件中即可**

```react
function Position(props) {
    return (
        <p>
            X:{props.x}
            Y:{props.y}
        </p>
    )
}
// 把position 组件来进行包装
let MousePosition = withMouse(Position)

class App extends React.Component {
    constructor(props) {
        super(props)
    }
    render() {
        return (
            <div>
                高阶组件
                <MousePosition></MousePosition>
            </div>
        )
    }
}
```

## 设置`displayName`

- 使用高阶组件存在的问题：得到两个组件的名称相同
- 原因：默认情况下，React使用组件名称作为`displayName`
- 解决方式：为高阶组件设置`displayName`，便于调试时区分不同的组件
- `displayName的作用：用于设置调试信息(React Developer Tools信息)`
- 设置方式：

![](/assets/img/article/%E9%AB%98%E9%98%B6%E7%BB%84%E4%BB%B6-displayName.png)

## 传递props

- 问题：如果没有传递props，会导致props丢失问题
- 解决方式： 渲染`WrappedComponent`时，将state和props一起传递给组件

![](/assets/img/article/%E4%BC%A0%E9%80%92props.png)

## 小结

- 组件通讯是构建React应用必不可少的一环
- props的灵活性让组件更加强大
- 状态提升是React组件的常用模式
- 组件生命周期有助于理解组件的运行过程
- 钩子函数让开发者可以在特定的时机执行某些功能
- `render props` 模式和高阶组件都可以实现组件状态逻辑的复用
- 组件极简模型： `(state,props) => UI`

# React原理

## 目标

- 能够知道`setState()`更新数据是异步的
- 能够知道JSX语法的转化过程

## `setState()`说明 （★★★）

### 更新数据

- `setState()`更新数据是异步的
- 注意：使用该语法，后面的`setState`不要依赖前面`setState`的值
- 多次调用`setState`，只会触发一次render

### 推荐语法 

- 推荐：使用 `setState((state,props) => {})` 语法
- 参数state： 表示最新的state
- 参数props： 表示最新的props

![](/assets/img/article/%E6%8E%A8%E8%8D%90%E8%AF%AD%E6%B3%95.png)



### 第二个参数

- 场景：在状态更新(页面完成重新渲染)后立即执行某个操作
- 语法：`setState(update[,callback])`

![](/assets/img/article/%E7%AC%AC%E4%BA%8C%E4%B8%AA%E5%8F%82%E6%95%B0.png)

## JSX语法的转化过程 （★★★）

- JSX仅仅是`createElement()` 方法的语法糖(简化语法)
- JSX语法被 @babel/preset-react 插件编译为`createElement()` 方法
- React 元素： 是一个对象，用来描述你希望在屏幕上看到的内容

![](/assets/img/article/%E8%AF%AD%E6%B3%95%E7%B3%96.png)