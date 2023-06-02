---
title: 6.7 api 发送注册请求
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: 976e09d8
date: 2022-10-31 11:03:07
---

# 6.7 api 发送注册请求

## 实现步骤：

---

### 第 1 步：安装 vscode 插件 Json to Dart Model

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_2eRAK11MT4.png" alt="img" style="zoom:33%;" />

### 第 2 步：生成请求 model

复制请求 json

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_yD4DZPUsZu.png" alt="img" style="zoom:33%;" />

```dart
{
    "username": "ducafecat5",
    "password": "123456",
    "email": "ducafecat5@gmail.com",
    "first_name": "ducafecat5",
    "last_name": ""
}
```

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_KqEEl-BWhH.png" alt="img" style="zoom:33%;" />

> 如果你是剪贴板的选 `From ClipBoard`
>
> 输入 `user_register`

生成文件 `lib/common/models/request/user_register.dart`

```dart
/// 用户注册请求
class UserRegisterReq {
  String? username;
  String? password;
  String? email;
  String? firstName;
  String? lastName;

  UserRegisterReq({
    this.username,
    this.password,
    this.email,
    this.firstName,
    this.lastName,
  });

  factory UserRegisterReq.fromJson(Map<String, dynamic> json) {
    return UserRegisterReq(
      username: json['username'] as String?,
      password: json['password'] as String?,
      email: json['email'] as String?,
      firstName: json['first_name'] as String?,
      lastName: json['last_name'] as String?,
    );
  }

  Map<String, dynamic> toJson() => {
        'username': username,
        'password': password,
        'email': email,
        'first_name': firstName,
        'last_name': lastName,
      };
}
```

> 类名 `UserRegister` 改成 `UserRegisterReq`

### 第 3 步：检查是否创建成功

根据接口规范新增成功返回 `statusCode` `201`, 所以我们只要判断返回状态即可

详见 api 规范

### 第 4 步：api 编写

lib/common/api/user.dart

```dart
/// 用户 api
class UserApi {
  /// 注册
  static Future<bool> register(UserRegisterReq? req) async {
    var res = await WPHttpService.to.post(
      '/users/register',
      data: req,
    );

    if (res.statusCode == 201) {
      return true;
    }
    return false;
  }
}
```

### 第 5 步：跳转 pin 界面

lib/pages/system/register/controller.dart

```dart
  // 注册
  void onSignUp() {
    if ((formKey.currentState as FormState).validate()) {
      // aes 加密密码
      // var password = EncryptUtil().aesEncode(passwordController.text);
      var password = passwordController.text;

      //验证通过
      Get.offNamed(
        RouteNames.systemRegisterPin,
        arguments: UserRegisterReq(
          username: userNameController.text,
          email: emailController.text,
          firstName: firstNameController.text,
          lastName: lastNameController.text,
          password: password,
        ),
      );
    }
  }
```

### 最后：pin 发送请求

lib/pages/system/register_pin/controller.dart

```dart
  // 注册界面传值
	UserRegisterReq? req = Get.arguments;
```

```dart
  // 注册
  Future<void> _register() async {
    try {
      Loading.show();

      // 暂时提交，后续改 aes 加密后处理
      // bool isOk = await UserApi.register(req);
      // if (isOk) {
      //   Loading.success(
      //       LocaleKeys.commonMessageSuccess.trParams({"method": "Register"}));
      //   Get.back(result: true);
      // }

      // 提示成功
      Loading.success(
          LocaleKeys.commonMessageSuccess.trParams({"method": "Register"}));
      Get.back(result: true);
    } finally {
      Loading.dismiss();
    }
  }
```

```dart
  // 按钮提交
  void onBtnSubmit() {
    _register();
  }
```

> `Loading.show` 会显示个 loading 的对话框，最后 `Loading.dismiss();` 关闭

> 提交代码到 git
