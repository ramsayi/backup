---
title: 5.3 Skip、Next、Start 按钮联动
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: ccb6788a
date: 2022-10-31 11:03:07
---

# 5.3 Skip、Next、Start 按钮联动

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image-20220713135816995.png" alt="image-20220713135816995" style="zoom:33%;" />

## 实现步骤：

---

### 第 1 步：控制器

lib/pages/system/welcome/controller.dart

```dart
  List<WelcomeModel>? items; // 滚动集合
  int currentIndex = 0; // 当前项
  bool isShowStart = false; // 是否显示 Start
  CarouselController carouselController = CarouselController(); // slider 控制器

	// 当前位置发生变化
  void onPageChanged(int index) {
    currentIndex = index;
    isShowStart = currentIndex == 2;
    update(['slider', 'bar']);
  }

	// 去首页
  void onToMain() {
    Get.offAllNamed(RouteNames.systemMain);
  }

	// 下一个
  void onNext() {
    carouselController.nextPage();
  }
```

### 第 2 步：视图

lib/pages/system/welcome/view.dart

```dart
  // slider
  Widget _buildSlider() {
    return GetBuilder<WelcomeController>(
      id: "slider",
      init: controller,
      builder: (controller) => controller.items == null
          ? const SizedBox()
          : WelcomeSliderWidget(
              controller.items!,
              carouselController: controller.carouselController,
              onPageChanged: controller.onPageChanged,
            ),
    );
  }

  // bar
  // skip + indicator + next
  Widget _buildBar() {
    return GetBuilder<WelcomeController>(
      id: "bar",
      init: controller,
      builder: (controller) {
        return controller.isShowStart
            ?
            // 开始
            ButtonWidget.primary(
                LocaleKeys.welcomeStart.tr,
                onTap: controller.onToMain,
              ).tight(
                width: double.infinity,
                height: 50.h,
              )
            : <Widget>[
                // 跳过
                ButtonWidget.text(
                  LocaleKeys.welcomeSkip.tr,
                  onTap: controller.onToMain,
                ),
                // 指示标
                SliderIndicatorWidget(
                  length: 3,
                  currentIndex: controller.currentIndex,
                ),
                // 下一页
                ButtonWidget.text(
                  LocaleKeys.welcomeNext.tr,
                  onTap: controller.onNext,
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

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_Tlsj0M0bPP.png" alt="img" style="zoom:25%;" />

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_rviIoeDXsT.png" alt="img" style="zoom:25%;" />

> 提交代码到 git
