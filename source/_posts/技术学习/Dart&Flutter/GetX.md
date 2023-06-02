---
title: GetX
tags:
  - Dart
  - Flutter
  - Getx
categories:
  - 技术学习
  - Dart&Flutter
copyright: false
abbrlink: 4778d367
cover: '/assets/img/post/getx.webp'
date: 2022-09-18 10:35:27
---

# 前言

> 使用Bloc的时候，有一个让我至今为止十分在意的问题，无法真正的跨页面交互！在反复的查阅官方文档后，使用一个全局Bloc的方式，实现了“伪”跨页面交互，详细可查看：[flutter_bloc使用解析](https://juejin.cn/post/6856268776510504968)；fish_redux的广播机制是可以比较完美的实现跨页面交互的，我也写了一篇几万字文章介绍如何使用该框架：[fish_redux使用详解](https://juejin.cn/post/6860029460524040199)，redux层次划分是比较细的，写起来会很费劲；最近尝试了GetX相关功能，解决了我的相当一部分痛点

> 把整篇文章写完后，我马上把自己的一个demo里面所有Bloc代码全用GetX替换，且去掉了Fluro框架；感觉用Getx虽然会省掉大量的模板代码，但还是有些重复工作：创建文件夹，创建几个必备文件，写那些必须要写的初始化代码和类；略微繁琐，**为了对得起GetX给我开发带来的巨大便利，我就花了一些时间，给它写了一个插件！** 上面这重复的代码，文件，文件夹统统能一键生成！

**GetX相关优势**

- 依赖注入
  - GetX是通过依赖注入的方式，存储相应的XxxGetxController；已经脱离了InheritedWidget那一套玩法，自己手动去管理这些实例，使用场景被大大拓展
  - 简单的思路，却能产生深远的影响：优雅的跨页面功能便是基于这种设计而实现的、获取实例无需BuildContext、GetBuilder自动化的处理及其减少了入参等等
- 跨页面交互
  - 这绝对是GetX的一个优点！对于复杂的生产环境，跨页面交互的场景，实在太常见了，GetX的跨页面交互，实现的也较为优雅
- 路由管理
  - getx内部实现了路由管理，而且用起来，非常简单！bloc没实现路由管理，我不得不找一个star量高的路由框架，就选择了fluro，但是不得不吐槽下，fluro用起来真的很折磨人，每次新建一个页面，最让我抗拒的就是去写fluro路由代码，横跨几个文件来回写，头皮发麻
  - GetX实现了动态路由传参，也就是说直接在命名路由上拼参数，然后能拿到这些拼在路由上的参数，也就是说用flutter写H5，直接能通过Url传值，OMG！可以无脑舍弃复杂的fluro了
- 实现了全局BuildContext
- 国际化，主题实现

如果深度使用过Provider，Bloc这类依赖InheritedWidget建立起的状态管理框架；再看看GetX内部实现思想，就能发现，他们已经是俩种体系的东西了

对此，我来抛出一些问题：InheritedWidget存在什么缺点？为什么其数据传递和路由设计思想对立？为什么getx使用依赖注入？getx的obx自动刷新黑魔法是个什么鬼？

- 对这些感兴趣的小伙伴，可以看看：[Flutter GetX深度剖析 | 我们终将走出自己的路（万字图文）](https://juejin.cn/post/6984593635681517582)

下来将全面的介绍GetX的使用，文章也不分篇水阅读量了，力求一文写清楚，方便大家随时查阅

# 准备

## 引入

- 首先导入GetX的插件

```dart
# getx 状态管理框架 https://pub.flutter-io.cn/packages/get
# 非空安全最后一个版本（flutter 2.0之前版本）
get: ^3.26.0
    
# 空安全版本 最新版本请查看  https://pub.flutter-io.cn/packages/get
get: ^4.3.8

```

**GetX地址**

- Github：[jonataslaw/getx](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fjonataslaw%2Fgetx)
- Pub：[get](https://link.juejin.cn/?target=https%3A%2F%2Fpub.dev%2Fpackages%2Fget)

## 主入口配置

- 只需要将`MaterialApp`改成`GetMaterialApp`即可

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      home: CounterGetPage(),
    );
  }
}

```

- 各模块导包，均使用下面包即可

```dart
import 'package:get/get.dart';

```

## 插件

这个getx代码生成插件，我花了不少精力去完善，功能已经比较齐全了，希望对大家有所帮助。

欢迎大家提issue，提issue之前，请务必认真查看文档：[GetX代码生成IDEA插件，超详细功能讲解](https://juejin.cn/post/7005003323753365517)，确保想提的需求，在本插件里面未被实现；上次有个老哥给我连开三个issue，提的需求都是早已实现的功能。。。

### 说明

> **插件地址**

- Github：[getx_template](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fxdd666t%2Fgetx_template)
- Jetbrains：[getx_template](https://link.juejin.cn/?target=https%3A%2F%2Fplugins.jetbrains.com%2Fplugin%2F15919-getx%2Fversions)

> **插件的功能含义**

- Model：生成GetX的模式
  - Default：默认模式，生成三个文件：state，logic，view
  - Easy：简单模式，生成俩个文件：logic，view
- Module Name：模块的名称，请使用大驼峰或小驼峰命名
- 插件详细功能说明，请查阅：[GetX代码生成IDEA插件，超详细功能讲解](https://juejin.cn/post/7005003323753365517)

### 安装

- 在设置里面选择：Plugins ---> 输入“getx”搜索 ---> 选择名字为：“GeX” ---> 然后安装 ---> 最后记得点击下“Apply”

![image-20210927092128051](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9935ebc5a8384f2faff7b48d728896c9~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

### 效果图

- 生成模板代码弹窗

![getx_new](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7e7b623b2e1e424a982ccc9301df6424~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

- 提供后缀名修改，也支持了持久化

![image-20210926111944785](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/be33ac035cc448fa8eff8616903a1704~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

- Alt + Enter ： 可以选择包裹Widget，有四种可选：GetBuilder、GetBuilder（Auto Dispose），Obx、GetX，大大方便开发哟(＾Ｕ＾)ノ~ＹＯ
  - 如果你发现某个页面，你的GetXController无法回收，可以使用 GetBuilder（Auto Dispose）Wrap 你的 Widget

![image-20210802160603092](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/30e14f564b6c427e9c65757811b53140~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

![image-20210802160631405](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/461c5cfa1eb746d881ced0dba1560343~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

- 快捷代码片段提示：我自己写了很多，也有一部分直接引用：

  getx-snippets-intelliJ

  - 输入 **getx** 前缀便有提示

![image-20210922111700625](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/64a2b143ea474c6480df5534687d8347~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

# 计数器

## 效果图

- [体验一下](https://link.juejin.cn/?target=https%3A%2F%2Fxdd666t.github.io%2Fflutter_use%2Fweb%2Findex.html%23%2FgetCounterRx)

![counter_getx](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/356a139dc86f49ea9aaad9ee29e7fe87~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

## 实现

**首先，当然是实现一个简单的计数器，来看GetX怎么将逻辑层和界面层解耦的**

- 来使用插件生成下简单文件
  - 模式选择：Easy
  - 功能选择：useFolder

![image-20210927092300651](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f59c98bcaac148099eadbbab05a4c2a5~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

来看下生成的默认代码，默认代码十分简单，详细解释放在俩种状态管理里

- logic

```dart
import 'package:get/get.dart';

class CounterGetLogic extends GetxController {

}

```

- view

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

import 'logic.dart';

class CounterGetPage extends StatelessWidget {
  final logic = Get.put(CounterGetLogic());

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}

```

### 简单状态管理

> GetBuilder：这是一个极其轻巧的状态管理器，占用资源极少！

- logic：先来看看logic层
  - 因为是处理页面逻辑的，加上Controller单词过长，也防止和Flutter自带的一些控件控制器弄混，所以该层用`logic`结尾，这里就定为了`logic`层
  - 当然这点随个人意向，写Event，Controller均可（插件生成代码，支持自定义通用后缀）

```dart
class CounterEasyLogic extends GetxController {
  var count = 0;

  void increase() {
    ++count;
    update();
  }
}

```

- view

```dart
class CounterEasyPage extends StatelessWidget {
  final logic = Get.put(CounterEasyLogic());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('计数器-简单式')),
      body: Center(
        child: GetBuilder<CounterEasyLogic>(builder: (logic) {
          return Text(
            '点击了 ${logic.count} 次',
            style: TextStyle(fontSize: 30.0),
          );
        }),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => logic.increase(),
        child: Icon(Icons.add),
      ),
    );
  }
}

```

- 分析下：GetBuilder这个方法
  - init：虽然上述代码没用到，但是，这个参数是存在在GetBuilder中的，因为在加载变量的时候就使用`Get.put()`生成了`CounterEasyGetLogic`对象，GetBuilder会自动查找该对象，所以，就可以不使用init参数
  - builder：方法参数，拥有一个入参，类型便是GetBuilder所传入泛型的类型
  - initState，dispose等：GetBuilder拥有StatefulWidget所有周期回调，可以在相应回调内做一些操作

### 响应式状态管理

> 当数据源变化时，将自动执行刷新组件的方法

- logic层
  - 这里变量数值后写`.obs`操作，是说明定义了该变量为响应式变量，当该变量数值变化时，页面的刷新方法将自动刷新
  - 基础类型，List，类都可以加`.obs`，使其变成响应式变量

```dart
class CounterRxLogic extends GetxController {
  var count = 0.obs;

  ///自增
  void increase() => ++count;
}

```

- view层

```dart
class CounterRxPage extends StatelessWidget {
  final logic = Get.put(CounterRxLogic());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('计数器-响应式')),
      body: Center(
        child: Obx(() {
          return Text(
            '点击了 ${logic.count.value} 次',
            style: TextStyle(fontSize: 30.0),
          );
        }),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => logic.increase(),
        child: Icon(Icons.add),
      ),
    );
  }
}

```

- 可以发现刷新组件的方法极其简单：`Obx()`，这样可以愉快的到处写定点刷新操作了
- Obx()方法刷新的条件
  - 只有当响应式变量的值发生变化时，才会会执行刷新操作，当某个变量初始值为：“test”，再赋值为：“test”，并不会执行刷新操作
  - 当你定义了一个响应式变量，该响应式变量改变时，包裹该响应式变量的Obx()方法才会执行刷新操作，其它的未包裹该响应式变量的Obx()方法并不会执行刷新操作，Cool！
- 来看下如果把整个类对象设置成响应类型，如何实现更新操作呢？
  - 下面解释来自官方README文档
  - 这里尝试了下，将整个类对象设置为响应类型，当你改变了类其中一个变量，然后执行更新操作，`只要包裹了该响应类变量的Obx()，都会实行刷新操作`，将整个类设置响应类型，需要结合实际场景使用

```dart
// model
// 我们将使整个类成为可观察的，而不是每个属性。
class User{
    User({this.name = '', this.age = 0});
    String name;
    int age;
}

// controller
final user = User().obs;
//当你需要更新user变量时。
user.update( (user) { // 这个参数是你要更新的类本身。
    user.name = 'Jonny';
    user.age = 18;
});
// 更新user变量的另一种方式。
user(User(name: 'João', age: 35));

// view
Obx(()=> Text("Name ${user.value.name}: Age: ${user.value.age}"));
// 你也可以不使用.value来访问模型值。
user().name; // 注意是user变量，而不是类变量（首字母是小写的）。

```

## 总结

**分析**

- Obx是配合Rx响应式变量使用、GetBuilder是配合update使用：请注意，这完全是俩套定点刷新控件的方案
  - 区别：前者响应式变量变化，Obx自动刷新；后者需要使用update手动调用刷新
- 每一个响应式变量，都需要生成对应的`GetStream`，占用资源大于基本数据类型，会对内存造成一定压力
- `GetBuilder`内部实际上是对StatefulWidget的封装，所以占用资源极小

**使用场景**

- 一般来说，对于大多数场景都是可以使用响应式变量的
- 但是，在一个包含了大量对象的List，都使用响应式变量，将生成大量的`GetStream`，必将对内存造成较大的压力，该情况下，就要考虑使用简单状态管理了
- 总的来说：推荐GetBuilder和update配合的写法
  - GetBuilder内置回收GetxController的功能，能避免一些无法自动回收GetxController的坑爹问题
    - `使用GetBuilder的自动回收：GetBuilder需要设置assignId: true；或使用插件一键Wrap Widget：GetBuilder（Auto Dispose）`
  - **使用Obx，相关变量定义初始化以及实体更新和常规写法不同，会对初次接触该框架的人，造成很大的困扰**
  - **getx的IDEA插件现已支持一键Wrap Widget生成GetBuilder，可以一定程度上提升你的开发效率**

# 跨页面交互

> 跨页面交互，在复杂的场景中，是非常重要的功能，来看看GetX怎么实现跨页面事件交互的

## 效果图

- [体验一下](https://link.juejin.cn/?target=https%3A%2F%2Fxdd666t.github.io%2Fflutter_use%2Fweb%2Findex.html%23%2FjumpOne)
- Cool，这才是真正的跨页面交互！下级页面能随意调用上级页面事件，且关闭页面后，下次重进，数据也很自然重置了（全局Bloc不会重置，需要手动重置）

![jump_getx](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/188439cfe00d45baba407f22e7602dd4~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

## 实现

### 页面一

常规代码

- logic
  - 这里的自增事件，是供其它页面调用的，该页面本身没使用

```dart
class GetJumpOneLogic extends GetxController {
  var count = 0;

  ///跳转到跨页面
  void toJumpTwo() {
    Get.toNamed(RouteConfig.getJumpTwo, arguments: {'msg': '我是上个页面传递过来的数据'});
  }

  ///跳转到跨页面
  void increase() {
    count = ++count;
    update();
  }
}

```

- view
  - 此处就一个显示文字和跳转功能

```dart
class GetJumpOnePage extends StatelessWidget {
  /// 使用Get.put()实例化你的类，使其对当下的所有子路由可用。
  final logic = Get.put(GetJumpOneLogic());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      appBar: AppBar(title: Text('跨页面-One')),
      floatingActionButton: FloatingActionButton(
        onPressed: () => logic.toJumpTwo(),
        child: const Icon(Icons.arrow_forward_outlined),
      ),
      body: Center(
        child: GetBuilder<GetJumpOneLogic>(
          builder: (logic) {
            return Text('跨页面-Two点击了 ${logic.count} 次',
                style: TextStyle(fontSize: 30.0));
          },
        ),
      ),
    );
  }
}

```

### 页面二

这个页面就是重点了

- logic
  - 将演示怎么调用前一个页面的事件
  - 怎么接收上个页面数据
  - 请注意，`GetxController`包含比较完整的生命周期回调，可以在`onInit()`接受传递的数据；如果接收的数据需要刷新到界面上，请在`onReady`回调里面接收数据操作，`onReady`是在`addPostFrameCallback`回调中调用，刷新数据的操作在`onReady`进行，能保证界面是初始加载完毕后才进行页面刷新操作的

```dart
class GetJumpTwoLogic extends GetxController {
  var count = 0;
  var msg = '';

  @override
  void onReady() {
    var map = Get.arguments;
    msg = map['msg'];
    update();

    super.onReady();
  }

  ///跳转到跨页面
  void increase() {
    count = ++count;
    update();
  }
}

```

- view
  - 加号的点击事件，点击时，能实现俩个页面数据的变换
  - 重点来了，这里通过`Get.find()`，获取到了之前实例化GetXController，获取某个模块的GetXController后就很好做了，可以通过这个GetXController去调用相应的事件，也可以通过它，拿到该模块的数据！

```dart
class GetJumpTwoPage extends StatelessWidget {
  final oneLogic = Get.find<GetJumpOneLogic>();
  final twoLogic = Get.put(GetJumpTwoLogic());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      appBar: AppBar(title: Text('跨页面-Two')),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          oneLogic.increase();
          twoLogic.increase();
        },
        child: const Icon(Icons.add),
      ),
      body: Center(
        child: Column(mainAxisSize: MainAxisSize.min, children: [
          //计数显示
          GetBuilder<GetJumpTwoLogic>(
            builder: (logic) {
              return Text('跨页面-Two点击了 ${twoLogic.count} 次',
                  style: TextStyle(fontSize: 30.0));
            },
          ),

          //传递数据
          GetBuilder<GetJumpTwoLogic>(
            builder: (logic) {
              return Text('传递的数据：${twoLogic.msg}',
                  style: TextStyle(fontSize: 30.0));
            },
          ),
        ]),
      ),
    );
  }
}

```

## 总结

GetX这种的跨页面交互事件，真的是非常简单了，侵入性也非常的低，不需要在主入口配置什么，在复杂的业务场景下，这样简单的跨页面交互方式，就能实现很多事了

# 进阶吧！计数器

> 我们可能会遇到过很多复杂的业务场景，在复杂的业务场景下，单单某个模块关于变量的初始化操作可能就非常多，在这个时候，如果还将state（状态层）和logic（逻辑层）写在一起，维护起来可能看的比较晕
>
> 这里将状态层和逻辑层进行一个拆分，这样在稍微大一点的项目里使用GetX，也能保证结构足够清晰了！

在这里就继续用计数器举例吧！

## 实现

此处需要划分三个结构了：state（状态层），logic（逻辑层），view（界面层）

- 这里使用插件生成下模板代码
  - Model：选择Default（默认）
  - Function：useFolder（默认选中）

![image-20211127151801015](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/001f2f9188b8436fb0d894f6e1369e3f~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

**来看下生成的模板代码**

- state

```dart
class GetCounterHighState {
  GetCounterHighState() {
    ///Initialize variables
  }
}

```

- logic

```dart
import 'package:get/get.dart';

import 'state.dart';

class GetCounterHighLogic extends GetxController {
  final GetCounterHighState state = GetCounterHighState();
}

```

- view

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

import 'logic.dart';

class GetCounterHighPage extends StatelessWidget {
  final logic = Get.put(GetCounterHighLogic());
  final state = Get.find<GetCounterHighLogic>().state;

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}

```

为什么写成这样三个模块，需要把State单独提出来，请速速浏览下方

### 改造

- state
  - 这里使用划分出来的state层，来统一管理所有的状态变量
  - 涉及到状态变量定义和Logic层彻底分开

```dart
class GetCounterHighState {
  late int count;

  GetCounterHighState() {
    count = 0;
  }
}

```

- logic
  - 逻辑层就比较简单，需要注意的是：开始时需要实例化状态类

```dart
class GetCounterHighLogic extends GetxController {
  final GetCounterHighState state = GetCounterHighState();

  ///自增
  void increase() {
    state.count = ++state.count;
    update();
  }
}

```

- view
  - 实际上view层，和之前的几乎没区别，区别的是把状态层给独立出来了
  - 因为`CounterHighGetLogic`被实例化，所以直接使用`Get.find<CounterHighGetLogic>()`就能拿到刚刚实例化的逻辑层，然后拿到state，使用单独的变量接收下
  - ok，此时：logic只专注于触发事件交互，state只专注数据

```dart
class GetCounterHighPage extends StatelessWidget {
  final logic = Get.put(GetCounterHighLogic());
  final state = Get.find<GetCounterHighLogic>().state;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('计数器-进阶版')),
      body: Center(
        child: GetBuilder<GetCounterHighLogic>(
          builder: (logic) {
            return Text(
              '点击了 ${state.count} 次',
              style: TextStyle(fontSize: 30.0),
            );
          },
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => logic.increase(),
        child: Icon(Icons.add),
      ),
    );
  }
}

```

### 对比

> 看了上面的改造，屏幕前的你可能想吐槽了：坑比啊，之前简简单单的逻辑层，被拆成俩个，还搞得这么麻烦，你是猴子请来的逗比吗？
>
> 大家先别急着吐槽，当业务过于复杂，state层，也是会维护很多东西的，让我们看看下面的一个小栗子，下面实例代码是不能直接运行的，想看详细运行代码，请查看项目：[flutter_use](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fxdd666t%2Fflutter_use)

- state

```dart
class MainState {
  ///选择index
  late int selectedIndex;

  ///控制是否展开
  late bool isUnfold;

  ///是否缩放
  late bool isScale;

  ///分类按钮数据源
  late List<BtnInfo> list;

  ///Navigation的item信息
  late List<BtnInfo> itemList;

  ///PageView页面
  late List<Widget> pageList;
  late PageController pageController;

  MainState() {
    //初始化index
    selectedIndex = 0;
    //默认不展开
    isUnfold = false;
    //默认不缩放
    isScale = false;
    //PageView页面
    pageList = [
      KeepAlivePage(FunctionPage()),
      KeepAlivePage(ExamplePage()),
      KeepAlivePage(SettingPage()),
    ];
    //item栏目
    itemList = [
      BtnInfo(
        title: "功能",
        icon: Icon(Icons.bubble_chart),
      ),
      BtnInfo(
        title: "范例",
        icon: Icon(Icons.opacity),
      ),
      BtnInfo(
        title: "设置",
        icon: Icon(Icons.settings),
      ),
    ];
    //页面控制器
    pageController = PageController();
  }
}

```

- logic

```dart
class MainLogic extends GetxController {
  final state = MainState();

  @override
  void onInit() {
    ///初始化应用信息
    InitConfig.initApp(Get.context);
    super.onInit();
  }

  ///切换tab
  void switchTap(int index) {
    state.selectedIndex = index;
    state.pageController.jumpToPage(index);
    update();
  }

  ///是否展开侧边栏
  void onUnfold(bool isUnfold) {
    state.isUnfold = !state.isUnfold;
    update();
  }

  ///是否缩放
  void onScale(bool isScale) {
    state.isScale = !state.isScale;
    update();

    initWindow(scale: isScale ? 1.25 : 1.0);
  }
}

```

- view

```dart
class MainPage extends StatelessWidget {
  final MainLogic logic = Get.put(MainLogic());
  final MainState state = Get.find<MainLogic>().state;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      body: Row(children: [
        ///侧边栏区域
        GetBuilder<MainLogic>(
          builder: (logic) {
            return SideNavigation(
              selectedIndex: state.selectedIndex,
              isUnfold: state.isUnfold,
              isScale: state.isScale,
              sideItems: state.itemList,
              //点击item
              onItem: (index) => logic.switchTap(index),
              //展开侧边栏
              onUnfold: (isUnfold) => logic.onUnfold(isUnfold),
              //缩放整体布局
              onScale: (isScale) => logic.onScale(isScale),
            );
          },
        ),

        ///Expanded占满剩下的空间
        Expanded(
          child: PageView.builder(
            physics: NeverScrollableScrollPhysics(),
            itemCount: state.pageList.length,
            itemBuilder: (context, index) => state.pageList[index],
            controller: state.pageController,
          ),
        )
      ]),
    );
  }
}

```

从上面可以看出，state层里面的状态已经较多了，当某些模块涉及到大量的：提交表单数据，跳转数据，展示数据等等，state层的代码会相当的多，相信我，真的是非常多，一旦业务发生变更，还要经常维护修改，就蛋筒了

在复杂的业务下，将状态层（state）和业务逻辑层（logic）分开，绝对是个明智的举动

## 最后

- 该模块的效果图就不放了，和上面计数器效果一模一样，想体验一下，可点击：[体验一下](https://link.juejin.cn/?target=https%3A%2F%2Fxdd666t.github.io%2Fflutter_use%2Fweb%2Findex.html%23%2FcounterHighGet)
- 简单的业务模块，可以使用俩层结构：logic，view；复杂的业务模块，推荐使用三层结构：state，logic，view

# Binding的使用

## 说明

大家可能发现了，插件上增加了addBinding的功能

![image-20210927093135423](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/865fd00f69fc4f799648c09a1b3edcda~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

再加上getx的demo也用了binding，想必各位靓仔就非常想使用这个功能

这个功能实际的作用非常简单

- 统一管理单模块使用的GetXController
- binding模块需要在getx路由页面进行绑定；进入页面的时候，统一懒注入binding模块的GetXController

这样做当然有好处

- 可以统一管理复杂模块的多个GetXController

请注意

- 不建议在Get.to()方法里面进行binding绑定
  - 如果存在多个页面跳转到存在binding页面，你的每个Get.to()方法都需要绑定
  - 这样极其容易出bug，对后面接盘的人，十分不友好
- 使用binding，你理应使用getx的命名路由

**郑重申明：不使用binding，并不会对功能有任何的影响**

## 使用

> **首先必须搭建好路由模块**

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      initialRoute: RouteConfig.testOne,
      getPages: RouteConfig.getPages,
    );
  }
}

class RouteConfig {
  static const String testOne = "/testOne";
  static const String testTwo = "/testOne/testTwo";

  static final List<GetPage> getPages = [
    GetPage(
      name: testOne,
      page: () => TestOnePage(),
      binding: TestOneBinding(),
    ),
    GetPage(
      name: testTwo,
      page: () => TestTwoPage(),
      binding: TestTwoBinding(),
    ),
  ];
}

```

> **创建页面模块**

- 选中addBinding功能

![image-20210927093312584](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a096e86c22af4b3496c0e188185770ce~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

- 创建TestOne

```dart
///logic层
class TestOneLogic extends GetxController {
  void jump() => Get.toNamed(RouteConfig.testTwo);
}

///view层
class TestOnePage extends StatelessWidget {
  final logic = Get.find<TestOneLogic>();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('页面一')),
      body: Center(child: Text('页面一', style: TextStyle(fontSize: 30.0))),
      floatingActionButton: FloatingActionButton(
        onPressed: () => logic.jump(),
        child: Icon(Icons.arrow_forward),
      ),
    );
  }
}

///binding层
class TestOneBinding extends Bindings {
  @override
  void dependencies() {
    Get.lazyPut(() => TestOneLogic());
  }
}

```

- TestTwo

```dart
///logic层
class TestTwoLogic extends GetxController {

}

///view层
class TestTwoPage extends StatelessWidget {
  final logic = Get.find<TestTwoLogic>();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('页面二')),
      body: Center(child: Text('页面二', style: TextStyle(fontSize: 30.0))),
    );
  }
}

///binding层
class TestTwoBinding extends Bindings {
  @override
  void dependencies() {
    Get.lazyPut(() => TestTwoLogic());
  }
}

```

## 总结

这边我写了一个极其简单的范例，仅仅是个跳转页面的功能，我觉得，应该可以展示binding的功能了

- 就是统一管理某个模块需要注入的多个GetXController
- 请注意，该注入是懒注入，只有使用了 find + 对应的泛型，才会被真正的注入的getx的全局map实例里

实际上，手动写binding文件，还是有点麻烦，写了binding，view层的使用也需要做相应的变动

铁汁们，为了帮你们节省点开发时间，这点浪费你们生命且没什么技术含量的事情，已经在插件里帮你完成

- 有需要的，选中addBinding功能即可
- GetPage里面绑定binding的操作，只能麻烦你们自己动下手了，项目结构千变万化，这玩意没法定位

# 路由管理

**GetX实现了一套用起来十分简单的路由管理，可以使用一种极其简单的方式导航，也可以使用命名路由导航**

**关于简单路由和命名路由的区别**

- 简单路由：十分简单，看下下面的例子

```dart
Get.to(SomePage());

```

- 命名路由
  - 在web上，可以直接通过命名的url直接导航页面
  - 实现路由拦截的操作，举一个官方文档的例子：很轻松的实现了一个未登录，跳转登录页面功能

```dart
GetStorage box = GetStorage();

GetMaterialApp(
  getPages: [
    GetPage(name: '/', page:(){
      return box.hasData('token') ? Home() : Login();
    })
  ]
)

```

## 简单路由

- 主入口配置

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      home: MainPage(),
    );
  }
}

```

- 路由的相关使用
  - 使用是非常简单，使用Get.to()之类api即可，此处简单演示，详细api说明，放在本节结尾

```dart
//跳转新页面
Get.to(SomePage());

```

## 命名路由导航

**这里是推荐使用命名路由导航的方式**

- 统一管理起了所有页面
- 在app中可能感受不到，但是在web端，加载页面的url地址就是命名路由你所设置字符串，也就是说，在web中，可以直接通过url导航到相关页面

下面说明下，如何使用

- 首先，在主入口出配置下

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      initialRoute: RouteConfig.main,
      getPages: RouteConfig.getPages,
    );
  }
}

```

- RouteConfig类
  - 下面是我的相关页面，和其映射的页面，请根据自己的页面进行相关编写

```dart
class RouteConfig {
  ///主页面
  static const String main = "/";

  ///演示SmartDialog控件 喜马拉雅  dialog页面
  static const String smartDialog = "/smartDialog";
  static const String himalaya = "/himalaya";
  static const String dialog = "/dialog";

  ///bloc计数器模块 Bloc跨页面传递事件
  static const String blCubitCounterPage = "/blCubitCounterPage";
  static const String blBlocCounterPage = "/blBlocCounterPage";
  static const String cubitSpanOne = "/cubitSpanOne";
  static const String cubitSpanTwo = "/cubitSpanOne/cubitSpanTwo";
  static const String streamPage = "/streamPage";
  static const String blCustomBuilderPage = "/blCustomBuilderPage";
  static const String counterEasyCPage = "/counterEasyCPage";

  ///测试布局页面
  static const String testLayout = "/testLayout";

  ///GetX 计数器  跨页面交互
  static const String getCounterRx = "/getCounterRx";
  static const String getCounterEasy = "/counterEasyGet";
  static const String getCounterHigh = "/counterHighGet";
  static const String getJumpOne = "/jumpOne";
  static const String getJumpTwo = "/jumpOne/jumpTwo";
  static const String getCounterBinding = "/getCounterBinding";
  static const String counterEasyXBuilderPage = "/counterEasyXBuilder";
  static const String counterEasyXEbxPage = "/counterEasyXEbx";

  ///Provider
  static const String proEasyCounterPage = "/proEasyCounterPage";
  static const String proHighCounterPage = "/proHighCounterPage";
  static const String proSpanOnePage = "/proSpanOnePage";
  static const String proSpanTwoPage = "/proSpanOnePage/proSpanTwoPage";
  static const String testNotifierPage = "/testNotifierPage";
  static const String customBuilderPage = "/customBuilderPage";
  static const String counterEasyPPage = "/counterEasyPPage";
  static const String counterGlobalEasyPPage = "/counterGlobalEasyPPage";

  ///别名映射页面
  static final List<GetPage> getPages = [
    GetPage(name: main, page: () => MainPage()),
    GetPage(name: dialog, page: () => DialogPage()),
    GetPage(name: blCubitCounterPage, page: () => BlCubitCounterPage()),
    GetPage(name: blBlocCounterPage, page: () => BlBlocCounterPage()),
    GetPage(name: streamPage, page: () => StreamPage()),
    GetPage(name: blCustomBuilderPage, page: () => BlCustomBuilderPage()),
    GetPage(name: counterEasyCPage, page: () => CounterEasyCPage()),
    GetPage(name: testLayout, page: () => TestLayoutPage()),
    GetPage(name: smartDialog, page: () => SmartDialogPage()),
    GetPage(name: cubitSpanOne, page: () => CubitSpanOnePage()),
    GetPage(name: cubitSpanTwo, page: () => CubitSpanTwoPage()),
    GetPage(name: getCounterRx, page: () => GetCounterRxPage()),
    GetPage(name: getCounterEasy, page: () => GetCounterEasyPage()),
    GetPage(name: getCounterHigh, page: () => GetCounterHighPage()),
    GetPage(name: getJumpOne, page: () => GetJumpOnePage()),
    GetPage(name: getJumpTwo, page: () => GetJumpTwoPage()),
    GetPage(
      name: getCounterBinding,
      page: () => GetCounterBindingPage(),
      binding: GetCounterBinding(),
    ),
    GetPage(name: counterEasyXBuilderPage, page: () => EasyXCounterPage()),
    GetPage(name: counterEasyXEbxPage, page: () => EasyXEbxCounterPage()),
    GetPage(name: himalaya, page: () => HimalayaPage()),
    GetPage(name: proEasyCounterPage, page: () => ProEasyCounterPage()),
    GetPage(name: proHighCounterPage, page: () => ProHighCounterPage()),
    GetPage(name: proSpanOnePage, page: () => ProSpanOnePage()),
    GetPage(name: proSpanTwoPage, page: () => ProSpanTwoPage()),
    GetPage(name: testNotifierPage, page: () => TestNotifierPage()),
    GetPage(name: customBuilderPage, page: () => CustomBuilderPage()),
    GetPage(name: counterEasyPPage, page: () => CounterEasyPPage()),
    GetPage(name: counterGlobalEasyPPage, page: () => CounterGlobalEasyPPage()),
  ];
}

```

## 路由API

**请注意命名路由，只需要在api结尾加上`Named`即可，举例：**

- 默认：Get.to(SomePage());
- 命名路由：Get.toNamed(“/somePage”);

**详细Api介绍，下面内容来自GetX的README文档，进行了相关整理**

- 导航到新的页面

```dart
Get.to(NextScreen());
Get.toNamed("/NextScreen");

```

- 关闭SnackBars、Dialogs、BottomSheets或任何你通常会用Navigator.pop(context)关闭的东西

```dart
Get.back();

```

- 进入下一个页面，但没有返回上一个页面的选项（用于SplashScreens，登录页面等）

```dart
Get.off(NextScreen());
Get.offNamed("/NextScreen");

```

- 进入下一个界面并取消之前的所有路由（在购物车、投票和测试中很有用）

```dart
Get.offAll(NextScreen());
Get.offAllNamed("/NextScreen");

```

- 发送数据到其它页面

只要发送你想要的参数即可。Get在这里接受任何东西，无论是一个字符串，一个Map，一个List，甚至一个类的实例。

```dart
Get.to(NextScreen(), arguments: 'Get is the best');
Get.toNamed("/NextScreen", arguments: 'Get is the best');

```

在你的类或控制器上：

```dart
print(Get.arguments);
//print out: Get is the best

```

- 要导航到下一条路由，并在返回后立即接收或更新数据

```dart
var data = await Get.to(Payment());
var data = await Get.toNamed("/payment");

```

- 在另一个页面上，发送前一个路由的数据

```dart
Get.back(result: 'success');
// 并使用它，例：
if(data == 'success') madeAnything();

```

- 如果你不想使用GetX语法，只要把 Navigator（大写）改成 navigator（小写），你就可以拥有标准导航的所有功能，而不需要使用context，例如：

```dart
// 默认的Flutter导航
Navigator.of(context).push(
  context,
  MaterialPageRoute(
    builder: (BuildContext context) {
      return HomePage();
    },
  ),
);

// 使用Flutter语法获得，而不需要context。
navigator.push(
  MaterialPageRoute(
    builder: (_) {
      return HomePage();
    },
  ),
);

// get语法
Get.to(HomePage());

```

**动态网页链接**

- 这是一个非常重要的功能，在web端，可以`保证通过url传参数到页面`里

Get提供高级动态URL，就像在Web上一样。Web开发者可能已经在Flutter上想要这个功能了，Get也解决了这个问题。

```dart
Get.offAllNamed("/NextScreen?device=phone&id=354&name=Enzo");

```

在你的controller/bloc/stateful/stateless类上：

```dart
print(Get.parameters['id']);
// out: 354
print(Get.parameters['name']);
// out: Enzo

```

你也可以用Get轻松接收NamedParameters。

```dart
void main() {
  runApp(
    GetMaterialApp(
      initialRoute: '/',
      getPages: [
      GetPage(
        name: '/',
        page: () => MyHomePage(),
      ),
      GetPage(
        name: '/profile/',
        page: () => MyProfile(),
      ),
       //你可以为有参数的路由定义一个不同的页面，也可以为没有参数的路由定义一个不同的页面，但是你必须在不接收参数的路由上使用斜杠"/"，就像上面说的那样。
       GetPage(
        name: '/profile/:user',
        page: () => UserProfile(),
      ),
      GetPage(
        name: '/third',
        page: () => Third(),
        transition: Transition.cupertino  
      ),
     ],
    )
  );
}

```

发送命名路由数据

```dart
Get.toNamed("/profile/34954");

```

在第二个页面上，通过参数获取数据

```dart
print(Get.parameters['user']);
// out: 34954

```

现在，你需要做的就是使用Get.toNamed()来导航你的命名路由，不需要任何context(你可以直接从你的BLoC或Controller类中调用你的路由)，当你的应用程序被编译到web时，你的路由将出现在URL中。

# 资源释放

> **关于GetxController的资源释放，这个栏目的内容相当重要！**

## 资源未释放的场景

在我们使用GetX的时候，可能没什么GetxController未被释放的感觉，这种情况，是因为我们一般都是用了getx的那一套路由跳转api（Get.to、Get.toName...）之类：使用Get.toName，肯定需要使用GetPage；如果使用Get.to，是不需要在GetPage中注册的，Get.to的内部有一个添加到GetPageRoute的操作

通过上面会在GetPage注册可知，说明在我们跳转页面的时候，GetX会拿你到页面信息存储起来，加以管理，下面俩种场景会导致GetxController无法释放

- GetxController可被自动释放的条件
  - GetPage+Get.toName配套使用，可释放
  - 直接使用Get.to，可释放
- GetxController无法被自动释放场景
  - 未使用GetX提供的路由跳转：直接使用原生路由api的跳转操作
  - 这样会直接导致GetX无法感知对应页面GetxController的生命周期，会导致其无法释放

```dart
Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => XxxxPage()),
);

```

**由此，可从上面可以看出，GetxController无法被释放的场景：不使用GetX路由**

## 最优解

这里有个最优解方案，就算你不使用Getx路由，也能很轻松回收各个页面的GetXController，感谢 [@法的空间](https://juejin.cn/user/254742428916408/posts) 在评论里指出

- 手动让getx感知路由

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HomePage,
      ///此处配置下！
      navigatorObservers: [GetXRouterObserver()],
    );
  }
}

///自定义这个关键类！！！！！！
class GetXRouterObserver extends NavigatorObserver {
  @override
  void didPush(Route<dynamic> route, Route<dynamic>? previousRoute) {
    RouterReportManager.reportCurrentRoute(route);
  }

  @override
  void didPop(Route<dynamic> route, Route<dynamic>? previousRoute) async {
    RouterReportManager.reportRouteDispose(route);
  }
}

```

讲真的，这个原理其实很简单，但是思路很有趣；大家点进`reportCurrentRoute` 和 `reportRouteDispose` 这俩个方法，大概就知道是怎么回事了

- `reportCurrentRoute` 就是让当前的路由标定给GetX
- 当我们进入一个页面的时候，相应GetXController会进行初始化，最终会调用 `_startController<S>({String? tag})`方法
- `_startController`中会调用`RouterReportManager.appendRouteByCreate(i)`，将注入的GetXController都保存起来
- 保存在一个map中，key为当前路由`route`，value为HashSet，可以保存多个GetXController
- ok，路由关闭的时候，在`reportRouteDispose`方法中回收，key为当前`route`，遍历value中所有的GetXController回收
- 我giao，基于这种思路，大家能干很多事了！！！

## 折中方案

如果上面的最优解没法帮你解决GetXController的回收问题，你可能就遇到特殊的场景了，一般来说，分析分析你自己的代码，基本都能分析出来

如果懒得分析原因，就试试下面这种折中方案吧；颗粒度极小，针对单页面维度解决

### StatefulWidget方案

这边我模拟了上面场景，写了一个解决方案

- 第一个页面跳转

```dart
Navigator.push(
    Get.context,
    MaterialPageRoute(builder: (context) => AutoDisposePage()),
);

```

- 演示页面
  - 这地方地方必须要使用StatefulWidget，因为在这种情况，无法感知生命周期，就需要使用StatefulWidget生命周期
  - 在dispose回调处，把当前GetxController从整个GetxController管理链中删除即可

```dart
class AutoDisposePage extends StatefulWidget {
  @override
  _AutoDisposePageState createState() => _AutoDisposePageState();
}

class _AutoDisposePageState extends State<AutoDisposePage> {
  final AutoDisposeLogic logic = Get.put(AutoDisposeLogic());

  @override
  Widget build(BuildContext context) {
    return BaseScaffold(
      appBar: AppBar(title: const Text('计数器-自动释放')),
      body: Center(
        child: Obx(
          () => Text('点击了 ${logic.count.value} 次',
              style: TextStyle(fontSize: 30.0)),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => logic.increase(),
        child: const Icon(Icons.add),
      ),
    );
  }

  @override
  void dispose() {
    Get.delete<AutoDisposeLogic>();
    super.dispose();
  }
}

class AutoDisposeLogic extends GetxController {
  var count = 0.obs;

  ///自增
  void increase() => ++count;
}

```

> **看到这，你可能会想，啊这！怎么这么麻烦，我怎么还要写StatefulWidget，好麻烦！**
>
> **各位放心，这个问题，我也想到了，我特地在插件里面加上了自动回收的功能**

- 如果你写的页面无法被回收，记得勾选autoDispose
  - 怎么判断页面的GetxController是否能被回收呢？实际上很简单，上面的未被释放的场景已经描述的比较清楚了，不清楚的话，就再看看

![image-20210922112126153](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2355654627694c0cb003423565de737f~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

来看下代码，default模式一样可以的

- view

```dart
class AutoDisposePage extends StatefulWidget {
  @override
  _AutoDisposePageState createState() => _AutoDisposePageState();
}

class _AutoDisposePageState extends State<AutoDisposePage> {
  final AutoDisposeLogic logic = Get.put(AutoDisposeLogic());

  @override
    Widget build(BuildContext context) {
      return Container();
    }

  @override
  void dispose() {
    Get.delete<AutoDisposeLogic>();
    super.dispose();
  }
}

```

- logic

```dart
class AutoDisposeLogic extends GetxController {

}

```

### 优化StatefulWidget方案

上面的是个通用解决方法，你不需要额外的引入任何其它的东西；但是这种方案用到了StatefulWidget，代码多了一大坨，让我有点膈应

鄙人有着相当的强迫症，想了很久，从外部入手，我就写了一个通用控件，来对相应的GetXController进行回收

**GetBindWidget**

- 本控件含义：将GetXController和当前页面的生命周期绑定，页面关闭时，自动回收
- 该控件可以回收单个GetXController（bind参数），可以加上对应tag（tag参数）；也可以回收多个GetXController（binds），可以加上多个tag（tags参数，请和binds 一 一 对应；无tag的GetXController的，tag可以写成空字符：""）

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

/// GetBindWidget can bind GetxController, and when the page is disposed,
/// it can automatically destroy the bound related GetXController
///
///
/// Sample:
///
/// class SampleController extends GetxController {
///   final String title = 'My Awesome View';
/// }
///
/// class SamplePage extends StatelessWidget {
///   final controller = Get.put(SampleController());
///
///   @override
///   Widget build(BuildContext context) {
///     return GetBindWidget(
///       bind: controller,
///       child: Container(),
///     );
///   }
/// }
class GetBindWidget extends StatefulWidget {
  const GetBindWidget({
    Key? key,
    this.bind,
    this.tag,
    this.binds,
    this.tags,
    required this.child,
  })  : assert(
          binds == null || tags == null || binds.length == tags.length,
          'The binds and tags arrays length should be equal\n'
          'and the elements in the two arrays correspond one-to-one',
        ),
        super(key: key);

  final GetxController? bind;
  final String? tag;

  final List<GetxController>? binds;
  final List<String>? tags;

  final Widget child;

  @override
  _GetBindWidgetState createState() => _GetBindWidgetState();
}

class _GetBindWidgetState extends State<GetBindWidget> {
  @override
  Widget build(BuildContext context) {
    return widget.child;
  }

  @override
  void dispose() {
    _closeGetXController();
    _closeGetXControllers();

    super.dispose();
  }

  ///Close GetxController bound to the current page
  void _closeGetXController() {
    if (widget.bind == null) {
      return;
    }

    var key = widget.bind.runtimeType.toString() + (widget.tag ?? '');
    GetInstance().delete(key: key);
  }

  ///Batch close GetxController bound to the current page
  void _closeGetXControllers() {
    if (widget.binds == null) {
      return;
    }

    for (var i = 0; i < widget.binds!.length; i++) {
      var type = widget.binds![i].runtimeType.toString();

      if (widget.tags == null) {
        GetInstance().delete(key: type);
      } else {
        var key = type + (widget.tags?[i] ?? '');
        GetInstance().delete(key: key);
      }
    }
  }
}

```

- 使用非常的简单

```dart
/// 回收单个GetXController
class TestPage extends StatelessWidget {
  final logic = Get.put(TestLogic());

  @override
  Widget build(BuildContext context) {
    return GetBindWidget(
      bind: logic,
      child: Container(),
    );
  }
}

/// 回收多个GetXController
class TestPage extends StatelessWidget {
  final logicOne = Get.put(TestLogic(), tag: 'one');
  final logicTwo = Get.put(TestLogic());
  final logicThree = Get.put(TestLogic(), tag: 'three');

  @override
  Widget build(BuildContext context) {
    return GetBindWidget(
      binds: [logicOne, logicTwo, logicThree],
      tags: ['one', '', 'three'],
      child: Container(),
    );
  }
}

/// 回收日志
[GETX] Instance "TestLogic" has been created with tag "one"
[GETX] Instance "TestLogic" with tag "one" has been initialized
[GETX] Instance "TestLogic" has been created
[GETX] Instance "TestLogic" has been initialized
[GETX] Instance "TestLogic" has been created with tag "three"
[GETX] Instance "TestLogic" with tag "three" has been initialized
[GETX] "TestLogicone" onDelete() called
[GETX] "TestLogicone" deleted from memory
[GETX] "TestLogic" onDelete() called
[GETX] "TestLogic" deleted from memory
[GETX] "TestLogicthree" onDelete() called
[GETX] "TestLogicthree" deleted from memory

```

# 一些问题汇总

> 如果使用中，有比较坑的问题，希望大家在评论里提出来，我会在这个栏目汇总一下

1. **无法跳转重复页面**

- 另一种表现形式：使用Get.to（Get.toName）在系统Dialog上跳转页面，未关闭Dialog；返回，再跳转，会出现无法跳转的情况

debug了下to方法内部的运行，发现他用了一个preventDuplicates参数，限制跳转重复页面

- 为什么这样做？
  - 优点：能解决多次点击跳转按钮，跳转多个重复页面的问题
  - 缺点：限制了复杂业务跳转重复页面的场景

当然上面的缺点也不算是缺点，毕竟已经给了参数可以控制

- 跳转重复页面，可以这样写

```dart
Get.to(XxxxPage(), preventDuplicates: false);
// 或者
Get.toNamed('xxx',  preventDuplicates: false);

```

1. **使用PageView时，所有PageView页面控制器，全被初始化问题**

大家使用PageView，添加PageView页面，PageView页面用GetX构成，会发现所有的PageView页面控制器全被初始化了！并不是切换到某个页面时，对应页面的控制器才被初始化！

PageView切换到某个页面的时候，才会调用对应Page页面的build方法；`对于PageView页面，控制器的注入过程，不能写在类中了，需要将其移入到build方法中初始化。`

- 正常页面，注入写法（非PageView页面）

```dart
class CounterEasyGetPage extends StatelessWidget {
  final CounterEasyGetLogic logic = Get.put(CounterEasyGetLogic());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('计数器-简单式')),
      body: Center(
        child: GetBuilder<CounterEasyGetLogic>(
          builder: (logicGet) => Text(
            '点击了 ${logicGet.count} 次',
            style: TextStyle(fontSize: 30.0),
          ),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => logic.increase(),
        child: const Icon(Icons.add),
      ),
    );
  }
}

```

- PageView页面，初始化位置必须调整

```dart
class CounterEasyGetPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final CounterEasyGetLogic logic = Get.put(CounterEasyGetLogic());
  
    return Scaffold(
      appBar: AppBar(title: const Text('计数器-简单式')),
      body: Center(
        child: GetBuilder<CounterEasyGetLogic>(
          builder: (logicGet) => Text(
            '点击了 ${logicGet.count} 次',
            style: TextStyle(fontSize: 30.0),
          ),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => logic.increase(),
        child: const Icon(Icons.add),
      ),
    );
  }
}

```

- 大家如果觉得手动移太麻烦的话，也可以选中插件的 **isPageView** 功能

![image-20210927093414647](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3d3166f7d25e4c6493842daad09eeed1~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

# 最后

## 相关地址

- 文中DEMO地址：[flutter_use](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fxdd666t%2Fflutter_use)

- GetX插件地址：[getx_template](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fxdd666t%2Fgetx_template)

- Windows：

  Windows平台安装包

  - 密码：xdd666

## 系列文章

> 引流了，手动滑稽.png

- IDEA插件：[GetX代码生成IDEA插件，超详细功能讲解（透过现象看本质）](https://juejin.cn/post/7005003323753365517)
- GetX原理：[Flutter GetX深度剖析 | 我们终将走出自己的路（万字图文）](https://juejin.cn/post/6984593635681517582)
- 告别克苏鲁代码山：[Flutter 改善套娃地狱问题（仿喜马拉雅PC页面举例）](https://juejin.cn/post/6939774499399139336)
- 让Dialog拥有更多可能：[这一次，解决Flutter Dialog的各种痛点！](https://juejin.cn/post/7026150456673959943)
