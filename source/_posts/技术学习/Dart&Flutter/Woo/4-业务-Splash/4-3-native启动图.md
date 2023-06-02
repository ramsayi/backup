---
title: 4.3 native 启动图
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: 49b6eb92
date: 2022-10-31 11:03:07
---

# 4.3 native 启动图

## 实现步骤：

---

> flutter 引擎启动会有一点延迟，这时候会显示白屏，我们要做一个设备的启动图来优化下体验。

### 第 1 步：安装依赖包 flutter_native_splash

```bash
flutter pub add flutter_native_splash
```

### 第 2 步：配置 yaml

pubspec.yaml

```yaml
flutter_native_splash:
  color: "#ffffff"
  image: "assets/icons/launcher_android.png"
```

> `color` 启动图背景色，这里我设置白色 #ffffff
> `image` 启动图，可以放你的 logo，这张图背景透明

### 第 2 步：运行创建命令

```sh
flutter pub run flutter_native_splash:create
```

> 这将会生成各个平台的 splash ui 配置代码

### 第 4 步：启动后清除不用的资源

lib/global.dart

```dart
class Global {
  static Future<void> init() async {
    WidgetsBinding widgetsBinding = WidgetsFlutterBinding.ensureInitialized();
    FlutterNativeSplash.preserve(widgetsBinding: widgetsBinding);
    ...
  }
}
```

lib/pages/system/splash/controller.dart

```dart
  @override
  void onReady() {
    super.onReady();
    // 删除设备启动图
    FlutterNativeSplash.remove();
		initData();
  }
```

### 最后：运行

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_8p2VjfS3od.png" alt="img" style="zoom:25%;" />

> 提交代码到 git
