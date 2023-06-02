---
title: 1.9 显示名、App 图标
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: 78d54ae0
date: 2022-10-31 11:03:07
---

# 1.9 显示名、App 图标

## 一、显示名称修改：

---

### Android

android/app/src/main/AndroidManifest.xml

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.flutter_woo_commerce_getx_learn">
   <application
        android:label="Woo"
        android:name="${applicationName}"
        android:icon="@mipmap/ic_launcher">
```

> 修改 android:label 标签

### IOS

ios/Runner/Info.plist

```xml
  <key>CFBundleDisplayName</key>
  <string>Woo</string>
```

## 二、App 图标修改：

---

### 第 1 步：安装插件 flutter_launcher_icons_maker

```bash
flutter pub add flutter_launcher_icons_maker -d
```

### 第 2 步：pubspec.yaml 配置

复制图片到 assets/icons/launcher.png

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/launcher_ios_pa8OlFfxcO.png" alt="img" style="zoom:50%;" />

pubspec.yaml

```yaml
# app 图标
flutter_icons:
  android: true
  ios: true
  image_path: "assets/icons/launcher_ios.png"
  # image_path_ios: "assets/icons/launcher_ios.png"
  image_path_android: "assets/icons/launcher_android.png"
  adaptive_icon_background: "#ffffff"
```

> `android` `ios` true 覆盖资源文件
> `image_path` 图标图片 png
> `image_path_android` 指定 android 图片 png
> `adaptive_icon_background` 指定图标背景颜色

### 第 3 步：执行命令

在项目更目录执行

```bash
flutter packages get
flutter pub run flutter_launcher_icons_maker:main -f pubspec.yaml
```

android

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_qAVJk2P-HU.png" alt="img" style="zoom:50%;" />

ios

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_HjAAz9TZSU.png" alt="img" style="zoom: 33%;" />

> 提交代码到 git

```bash
git add .
git commit -m "icon & app name"
```
