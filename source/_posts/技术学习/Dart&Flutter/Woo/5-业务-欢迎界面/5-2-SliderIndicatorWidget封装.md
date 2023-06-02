---
title: 5.2 SliderIndicatorWidget 封装
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: 7c99c9ea
date: 2022-10-31 11:03:07
---

# 5.2 SliderIndicatorWidget 封装

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image-20220713134021845.png" alt="image-20220713134021845" style="zoom:33%;" />

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image-20220713134104294.png" alt="image-20220713134104294" style="zoom:33%;" />

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image-20220713134137620.png" alt="image-20220713134137620" style="zoom:33%;" />

## 实现步骤：

---

### 第 1 步：SliderIndicatorWidget 类

lib/common/components/slider_indicator.dart

```dart
import 'package:flutter/material.dart';
import 'package:flutter_woo_commerce_getx_learn/common/index.dart';

/// slider indicator 指示器
class SliderIndicatorWidget extends StatelessWidget {
  /// 个数
  final int length;

  /// 当前位置
  final int currentIndex;

  /// 颜色
  final Color color;

  /// 是否原型
  final bool isCircle;

  /// 对齐方式
  final MainAxisAlignment alignment;

  SliderIndicatorWidget({
    Key? key,
    required this.length,
    required this.currentIndex,
    Color? color,
    this.isCircle = false,
    this.alignment = MainAxisAlignment.center,
  })  : color = color ?? AppColors.primary,
        super(key: key);

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: alignment,

      // 采用 list.generate 方式生成 item 项
      children: List.generate(length, (index) {
        return Container(
          margin: const EdgeInsets.symmetric(horizontal: 3),
          // 圆型宽度 6 , 否则当前位置 15 , 其他位置 8
          width: !isCircle
              ? currentIndex == index
                  ? 15.0
                  : 8
              : 6,
          // 圆型高度 6 , 否则 4
          height: !isCircle ? 4 : 6,
          decoration: BoxDecoration(
            // 圆角 4
            borderRadius: const BorderRadius.all(Radius.circular(4)),
            // 非当前位置透明度 0.3
            color: currentIndex == index ? color : color.withOpacity(0.3),
          ),
        );
      }),
    );
  }
}
```

### 第 2 步：控制器

lib/pages/system/welcome/controller.dart

```dart
  // 当前位置
	int currentIndex = 0;

	// 当前位置发生改变
  void onPageChanged(int index) {
    currentIndex = index;
    update(['slider', 'bar']);
  }
```

### 第 3 步：视图

lib/pages/system/welcome/view.dart

```dart
	// 控制栏
	Widget _buildBar() {
    return GetBuilder<WelcomeController>(
      id: "bar",
      init: controller,
      builder: (controller) {
        return <Widget>[
                // 指示标
                SliderIndicatorWidget(
                  length: 3,
                  currentIndex: controller.currentIndex,
                ),
              ].toRow(
                mainAxisAlignment: MainAxisAlignment.spaceAround,
              );
      },
    );
  }

  // 内容页
  Widget _buildView() {
    return <Widget>[
      // slider切换
			buildSlider(),
      // 控制栏
			buildBar(),
    ]
        .toColumn(
          mainAxisAlignment: MainAxisAlignment.spaceAround,
        )
        .paddingAll(AppSpace.page);
  }
```

### 最后：运行

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_chYe83b7jS.png" alt="img" style="zoom:25%;" />

> 提交代码到 git
