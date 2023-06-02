---
title: 4.1 ScreenUtil 配置
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: 9b0c3626
date: 2022-10-31 11:03:07
---

# 4.1 ScreenUtil 配置

## 按比例适配屏幕

```dart
import 'package:flutter/material.dart';
import 'package:flutter_screenutil/flutter_screenutil.dart';

class ViewScreenPape extends StatelessWidget {
  const ViewScreenPape({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        width: 100.w,
        height: 100.w,
        color: Colors.amber,
        child: Text(
          "我是文字",
          style: TextStyle(
            fontSize: 20.sp,
          ),
        ),
      ),
    );
  }
}
```

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image-20220712143238499.png" alt="image-20220712143238499" style="zoom: 33%;" />

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image-20220712143309070.png" alt="image-20220712143309070" style="zoom:33%;" />

可以发现这个方案是按设备尺寸进行按比例适配

适配宽高和字体，这种方式用在非极端情况可以，

如果超长超高设备屏幕，需要媒体查询，就行优化交互显示。

## 实现步骤：

---

### 第 1 步：安装包 flutter_screenutil

执行

```bash
flutter pub add flutter_screenutil
```

### 最后：顶层包裹

> 注意配置下你的设计稿中设备的尺寸

lib/main.dart

```dart
  @override
  Widget build(BuildContext context) {
    return ScreenUtilInit(
      designSize: const Size(414, 896), // 设计稿中设备的尺寸(单位随意,建议dp,但在使用过程中必须保持一致)
      splitScreenMode: false, // 支持分屏尺寸
      minTextAdapt: false, // 是否根据宽度/高度中的最小值适配文字
      // 一般返回一个MaterialApp类型的Function()
      builder: (context, child) {
        return GetMaterialApp(
          title: 'Flutter Demo',

          // 样式
          theme: ConfigService.to.isDarkModel ? AppTheme.dark : AppTheme.light,

          // 路由
          initialRoute: RouteNames.stylesStylesIndex,
          getPages: RoutePages.list,
          navigatorObservers: [RoutePages.observer],

          // builder
          builder: (context, widget) {
            // 不随系统字体缩放比例
            return MediaQuery(
              data: MediaQuery.of(context).copyWith(textScaleFactor: 1.0),
              child: widget!,
            );
          },

          debugShowCheckedModeBanner: false,
        );
      },
    );
  }
```

> `builder` 中的处理是可选的

> 提交代码到 git
