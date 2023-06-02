---
title: 6.5 Pin 界面编写
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: e58a5d6d
date: 2022-10-31 11:03:07
---

# 6.5 Pin 界面编写

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image-20220715153443218.png" alt="image-20220715153443218" style="zoom: 33%;" />

## 实现步骤：

---

### 第 1 步：i18n 多语言

lib/common/i18n/locale_keys.dart

```dart
  // 注册PIN - register pin
  static const registerPinTitle = 'register_pin_title';
  static const registerPinDesc = 'register_pin_desc';
  static const registerPinFormTip = 'register_pin_form_tip';
  static const registerPinButton = 'register_pin_button';
```

lib/common/i18n/locales/locale_en.dart

```dart
  // 注册PIN - register pin
  LocaleKeys.registerPinTitle: 'Verification',
  LocaleKeys.registerPinDesc: 'we will send you a Pin to continue your account',
  LocaleKeys.registerPinFormTip: 'Pin',
  LocaleKeys.registerPinButton: 'Submit',
```

lib/common/i18n/locales/locale_zh.dart

```dart
  // 注册PIN - register pin
  LocaleKeys.registerPinTitle: '验证',
  LocaleKeys.registerPinDesc: '我们将向您发送PIN码以继续您的帐户',
  LocaleKeys.registerPinFormTip: 'Pin',
  LocaleKeys.registerPinButton: '提交',
```

### 第 2 步：pin 界面

lib/pages/system/register_pin/controller.dart

```dart
class RegisterPinController extends GetxController {
  RegisterPinController();

  // ping 文字输入控制器
  TextEditingController pinController = TextEditingController();

  // 表单 key
  GlobalKey formKey = GlobalKey<FormState>();

  // pin 触发提交
  void onPinSubmit(String val) {
    debugPrint("onPinSubmit: $val");
  }

  // 按钮提交
  void onBtnSubmit() {
  }

  // 按钮返回
  void onBtnBackup() {
    Get.back();
  }

  @override
  void onClose() {
    super.onClose();
    pinController.dispose();
  }
}
```

lib/pages/system/register_pin/view.dart

```dart
  // 表单页
  Widget _buildForm() {
    return Form(
      key: controller.formKey, //设置globalKey，用于后面获取FormState
      autovalidateMode: AutovalidateMode.onUserInteraction,
      child: <Widget>[
        // 提示文
        TextWidget.body1(LocaleKeys.registerPinFormTip.tr)
            .paddingBottom(20.w)
            .alignLeft(),

        // pin
        PinPutWidget(
          controller: controller.pinController,
          validator: controller.pinValidator, // 验证函数
          onSubmit: controller.onPinSubmit,
        ).paddingBottom(50.w),

        // 提交按钮
        ButtonWidget.primary(
          LocaleKeys.registerPinButton.tr,
          onTap: controller.onBtnSubmit,
        ).paddingBottom(AppSpace.listRow),

        // 返回按钮
        ButtonWidget.text(
          LocaleKeys.commonBottomCancel.tr,
          onTap: controller.onBtnBackup,
        ),

        // end
      ].toColumn(),
    ).paddingAll(AppSpace.card);
  }
```

```dart
  // 内容页
  Widget _buildView() {
    return SingleChildScrollView(
      child: <Widget>[
        // 头部标题
        PageTitleWidget(
          title: LocaleKeys.registerPinTitle.tr,
          desc: LocaleKeys.registerPinDesc.tr,
        ),

        // 表单
        _buildForm().card(),
      ]
          .toColumn(
            crossAxisAlignment: CrossAxisAlignment.start,
          )
          .paddingHorizontal(AppSpace.page),
    );
  }
```

### 第 3 步：验证

lib/pages/system/register_pin/controller.dart

```dart
  // 验证 pin
  String? pinValidator(val) {
    return val == '111111'
        ? null
        : LocaleKeys.commonMessageIncorrect.trParams({"method": "Pin"});
  }
```

> 默认 pin `111111`

lib/pages/system/register_pin/view.dart

```dart
        // pin
        PinPutWidget(
          controller: controller.pinController,
          validator: controller.pinValidator, // 验证函数
          onSubmit: controller.onPinSubmit,
        ).paddingBottom(50.w),
```

### 第 4 步：注册进入 Pin 界面

lib/pages/system/register/controller.dart

```dart
  // 注册
  void onSignUp() {
    if ((formKey.currentState as FormState).validate()) {
      // 验证通过提交数据
      Get.toNamed(RouteNames.systemRegisterPin);
    }
  }
```

### 最后：运行

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_l13zCXGt1c.png" alt="img" style="zoom:25%;" />

> 提交代码到 git
