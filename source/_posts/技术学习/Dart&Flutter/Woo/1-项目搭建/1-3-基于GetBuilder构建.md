---
title: 1.3 基于 GetBuilder 构建
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: ddc70a35
date: 2022-10-31 11:03:07
---

# 1.3 基于 GetBuilder 构建

## Getx Full 存在问题

- 虽然规范，但文件过多
- obs Obx 性能不好

## GetBuilder 的模块开发步骤

---

### 第 1 步: 创建 Splash 模块

> 右键菜单 “Getx: GetBuilder Page” 创建模块 “splash”

文件清单

```dart
└── splash
    ├── controller.dart
    ├── index.dart
    ├── view.dart
    └── widgets
```

| 名称            | 说明                 |
| --------------- | -------------------- |
| controller.dart | 控制器               |
| view.dart       | 页面                 |
| widgets         | 子组件（本模块私有） |
| index.dart      | 导包                 |

### 第 2 步: 阅读理解代码

controller.dart

```dart
import 'package:get/get.dart';

class SplashController extends GetxController {
  SplashController();

  _initData() {
    update(["splash"]);
  }

  void onTap() {}

  // @override
  // void onInit() {
  //   super.onInit();
  // }

  @override
  void onReady() {
    super.onReady();
    _initData();
  }

  // @override
  // void onClose() {
  //   super.onClose();
  // }

  // @override
  // void dispose() {
  //   super.dispose();
  // }
}
```

view.dart

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

import 'index.dart';

class SplashPage extends GetView<SplashController> {
  const SplashPage({Key? key}) : super(key: key);

  Widget _buildView() {
    return const Center(
      child: Text("SplashPage"),
    );
  }

  @override
  Widget build(BuildContext context) {
    return GetBuilder<SplashController>(
      init: SplashController(),
      id: "splash",
      builder: (_) {
        return Scaffold(
          appBar: AppBar(title: const Text("splash")),
          body: SafeArea(
            child: _buildView(),
          ),
        );
      },
    );
  }
}
```

> 就这两个文件，这次干净了

### 第 3 步: 尝试手动触发更新

- 加入点击更新 title 代码

lib/pages/system/splash/controller.dart

```dart
  String title = "";

  void onTap(int ticket) {
    title = "GetBuilder -> 点击了第 $ticket 个按钮";
    update(['splash_title']);
  }
```

lib/pages/system/splash/view.dart

```dart
  // 主视图
  Widget _buildView() {
    return Column(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: [
        // 文字标题
        GetBuilder<SplashController>(
          id: "splash_title",
          builder: (_) {
            return Center(
              child: Text(controller.title),
            );
          },
        ),

        // 按钮
        ElevatedButton(
          onPressed: () {
            controller.onTap(DateTime.now().microsecondsSinceEpoch);
          },
          child: const Text("立刻点击"),
        ),
      ],
    );
  }
```

- 路由注册

lib/common/routers/pages.dart

```dart
    GetPage(
      name: "/splash",
      page: () => const SplashPage(),
    ),
```

- 点击跳转 `splash`

lib/pages/system/login/view.dart1

```dart
  // 跳转
  ElevatedButton(
    onPressed: () {
      Get.toNamed("/splash");
    },
    child: const Text("跳转 splash"),
  ),
```

### 最后: 查看依赖 管理日志

我们进入模块后再退出，看下日志

```dart
[GETX] "SplashController" onDelete() called
[GETX] "SplashController" deleted from memory
[GETX] Instance "SplashController" already removed.
```

> 可以发现自动管理了内存加载释放，代码又进一步简洁了

> 提交代码到 git

```bash
git add .
git commit -m "GetBuilder Page 模块"
```
