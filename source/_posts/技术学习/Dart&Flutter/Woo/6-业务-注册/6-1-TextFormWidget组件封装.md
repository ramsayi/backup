---
title: 6.1 TextFormWidget 组件封装
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: 384d5ac4
date: 2022-10-31 11:03:07
---

# 6.1 TextFormWidget 组件封装

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image-20220715114802594.png" alt="image-20220715114802594" style="zoom:25%;" />

## 预备知识

### Form

`Form`继承自`StatefulWidget`对象，它对应的状态类为`FormState`。

`Form`类的定义：

```dart
class Form extends StatefulWidget {

  final Widget child;

  /// 决定Form所在的路由是否可以直接返回（如点击返回按钮），该回调返回一个Future对象，
  /// 如果 Future 的最终结果是false，则当前路由不会返回；
  /// 如果为true，则会返回到上一个路由。此属性通常用于拦截返回按钮。
  final WillPopCallback? onWillPop;

  /// Form的任意一个子FormField内容发生变化时会触发此回调。
  final VoidCallback? onChanged;

  /// 是否自动校验输入内容；当为true时，每一个子 FormField 内容发生变化时都会自动校验合法性，
  /// 并直接显示错误信息。否则，需要通过调用FormState.validate()来手动校验。
  final AutovalidateMode autovalidateMode;
```

### FormField

`Form`的子孙元素必须是`FormField`类型，`FormField`是一个抽象类，定义几个属性，`FormState`内部通过它们来完成操作，`FormField`部分定义如下：

```dart
class FormField<T> extends StatefulWidget {

  /// 保存回调
  /// [FormState.save].
  final FormFieldSetter<T>? onSaved;

  /// 验证回调
  final FormFieldValidator<T>? validator;

  /// 初始值
  final T? initialValue;

  /// 启用
  final bool enabled;

  /// 自动验证
  final AutovalidateMode autovalidateMode;
```

### TextFormField

为了方便使用，Flutter 提供了一个`TextFormField`组件，它继承自`FormField`类，也是`TextField`的一个包装类，所以除了`FormField`定义的属性之外，它还包括`TextField`的属性。

### FormState

`FormState`为`Form`的`State`类，可以通过`Form.of()`或`GlobalKey`获得。我们可以通过它来对`Form`的子孙`FormField`进行统一操作。我们看看其常用的三个方法：

- `FormState.validate()`：调用此方法后，会调用`Form`子孙`FormField的validate`回调，如果有一个校验失败，则返回 false，所有校验失败项都会返回用户返回的错误提示。

- `FormState.save()`：调用此方法后，会调用`Form`子孙`FormField`的`save`回调，用于保存表单内容

- `FormState.reset()`：调用此方法后，会将子孙`FormField`的内容清空。

## 实现步骤：

### 第 1 步：定义类参数

lib/common/widgets/text_form.dart

```dart
/// TextFormField 表单 输入框
class TextFormWidget extends StatefulWidget {
  /// 控制器
  final TextEditingController? controller;

  /// 输入框样式
  final InputDecoration? decoration;

  /// 验证函数
  final String? Function(String?)? validator;

  /// 自动焦点
  final bool? autofocus;

  /// 标题
  final String? labelText;

  /// 必须输入
  final bool? isMustBeEnter;

  /// 是否密码
  final bool? isObscure;

  /// 是否只读
  final bool? readOnly;

  /// 输入法类型
  final TextInputType? keyboardType;

  /// 输入格式定义
  final List<TextInputFormatter>? inputFormatters;

  /// 提示文字
  final String? hintText;

  /// 点击事件
  final Function()? onTap;

  const TextFormWidget({
    Key? key,
    this.controller,
    this.autofocus = false,
    this.labelText,
    this.isMustBeEnter = false,
    this.validator,
    this.isObscure = false,
    this.decoration,
    this.keyboardType,
    this.inputFormatters,
    this.readOnly = false,
    this.onTap,
    this.hintText,
  }) : super(key: key);

  @override
  _TextFormWidgetState createState() => _TextFormWidgetState();
}
```

### 第 2 步：build 函数

```dart
class _TextFormWidgetState extends State<TextFormWidget> {
  // 是否显示明文按钮
  bool _isShowObscureIcon = false;

  @override
  void initState() {
    super.initState();
    _isShowObscureIcon = widget.isObscure!;
  }

  @override
  Widget build(BuildContext context) {
    return TextFormField(
      onTap: widget.onTap, // 点击事件
      readOnly: widget.readOnly!, // 是否只读
      autofocus: widget.autofocus!, // 自动焦点
      keyboardType: widget.keyboardType, // 输入法类型
      controller: widget.controller, // 控制器
      decoration: widget.isObscure == true
          ? InputDecoration(
              hintText: widget.hintText, // 提示文字
              // 标题
              labelText: widget.isMustBeEnter == true
                  ? "* ${widget.labelText}"
                  : widget.labelText,
              // 密码按钮
              suffixIcon: IconButton(
                onPressed: () {
                  setState(() {
                    _isShowObscureIcon = !_isShowObscureIcon;
                  });
                },
                icon: Icon(
                  _isShowObscureIcon == true
                      ? Icons.visibility
                      : Icons.visibility_off,
                  size: 15,
                  color: AppColors.surfaceVariant,
                ),
              ),
            )
          : InputDecoration(
              hintText: widget.hintText,
              labelText: widget.isMustBeEnter == true
                  ? "* ${widget.labelText}"
                  : widget.labelText,
            ),
      // 校验
      validator: widget.validator,
      // 是否密码
      obscureText: _isShowObscureIcon,
      // 输入格式
      inputFormatters: widget.inputFormatters,
    );
  }
}
```

### 第 3 步：调试界面

lib/pages/styles/styles_index/view.dart

```dart
      // form 表单
      ListTile(
        onTap: () => Get.toNamed(RouteNames.stylesTextForm),
        title: const TextWidget.body1("form 表单"),
      ),
```

lib/pages/styles/text_form/controller.dart

```dart
  GlobalKey formKey = GlobalKey<FormState>();

  TextEditingController unameController = TextEditingController(text: "ducafecat");
  TextEditingController pwdController = TextEditingController(text: "123456");
```

```dart
  @override
  void onClose() {
    super.onClose();
    unameController.dispose();
    pwdController.dispose();
  }
```

lib/pages/styles/text_form/view.dart

```dart

  Widget _buildTextForm() {
    return Form(
        key: controller.formKey, //设置globalKey，用于后面获取FormState
        autovalidateMode: AutovalidateMode.onUserInteraction,
        child: <Widget>[
          TextFormWidget(
            // autofocus: true,
            keyboardType: TextInputType.emailAddress,
            controller: controller.unameController,
            labelText: "email",
            // validator: Validatorless.multiple([
            //   Validatorless.required("The field is obligatory"),
            //   Validatorless.min(6,
            //       "Length cannot be less than @size".trParams({"size": "6"})),
            //   Validatorless.max(
            //       18,
            //       "Length cannot be greater than @size"
            //           .trParams({"size": "18"})),
            //   Validatorless.email("The field must be an email"),
            // ]),
          ),
          TextFormWidget(
            controller: controller.pwdController,
            labelText: "password",
            isObscure: true,
            // validator: Validatorless.multiple([
            //   Validatorless.required("The field is obligatory"),
            //   Validatorless.min(6,
            //       "Length cannot be less than @size".trParams({"size": "6"})),
            //   Validatorless.max(
            //       18,
            //       "Length cannot be greater than @size"
            //           .trParams({"size": "18"})),
            // ]),
          ).marginOnly(
            bottom: 10,
          ),
          ButtonWidget.primary(
            "submit",
            onTap: () {
              if ((controller.formKey.currentState as FormState).validate()) {
                try {} finally {}
              }
            },
          ).tight(width: 100, height: 40),
        ].toColumn());
  }

  // 主视图
  Widget _buildView() {
    return SingleChildScrollView(
      child: _buildTextForm().padding(
        all: AppSpace.page,
      ),
    );
  }
```

### 最后：运行

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_ny4PA_RYba.png" alt="img" style="zoom:25%;" />

> 提交代码到 git
