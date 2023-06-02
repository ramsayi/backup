---
title: 1.5 config service 配置
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: f430c020
date: 2022-10-31 11:03:07
---

# 1.5 config service 配置

## 代码实现 ConfigService 全局配置管理

---

### 第 1 步: 安装依赖包 package_info_plus

```dart
flutter pub add package_info_plus
```

### 第 2 步: 创建 ConfigService

lib/common/services/config.dart

```dart
import 'package:get/get.dart';
import 'package:package_info_plus/package_info_plus.dart';

/// 配置服务
class ConfigService extends GetxService {
  // 这是一个单例写法
  static ConfigService get to => Get.find();

  PackageInfo? _platform;
  String get version => _platform?.version ?? '-';

  // 初始化
  Future<ConfigService> init() async {
    await getPlatform();
    return this;
  }

  Future<void> getPlatform() async {
    _platform = await PackageInfo.fromPlatform();
  }
}
```

> static ConfigService get to => Get.find(); 这是一个单例写法

### 第 3 步: 创建 Global

lib/global.dart

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

import 'common/index.dart';

class Global {
  static Future<void> init() async {
    WidgetsFlutterBinding.ensureInitialized();

    await Future.wait([
      Get.putAsync<ConfigService>(() async => await ConfigService().init()),
    ]).whenComplete(() {
    });
  }
}
```

> `Get.put` 方式直接注入

`WidgetsFlutterBinding.ensureInitialized();` 这个表示先就行原生端（ios android）插件注册，然后再处理后续操作，这样能保证代码运行正确。

修改 `main.dart`

```dart
Future<void> main() async {
  await Global.init();
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  ...
```

> 注意这里有个 `async` 同步的操作，保证 `Service` 正常初始化。

### 最后: 在 SplashPage 中调用

```dart
class SplashPage extends GetView<SplashController> {
  const SplashPage({Key? key}) : super(key: key);

  Widget _buildView() {
    return Center(
      child: Text("SplashPage - ${ConfigService.to.version}"),
    );
  }
```

注意看这里的 `ConfigService.to.version` 这是单例的调用，使用很便利。

运行后显示当前版本号

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_JM4yLZLi25.png" alt="img" style="zoom:25%;" />

> 提交代码到 git

```bash
git add .
git commit -m "config service"
```
