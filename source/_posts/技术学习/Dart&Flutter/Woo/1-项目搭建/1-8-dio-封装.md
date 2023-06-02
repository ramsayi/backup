---
title: 1.8 dio 封装
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: 685b06f5
date: 2022-10-31 11:03:07
---

# 1.8 dio 封装

## 参考

https://pub.dev/packages/dio

https://github.com/flutterchina/dio/blob/master/README-ZH.md

## 实现步骤：

---

> 开始之前请阅读 API 设计规范说明

### 第 1 步：安装插件 dio

```bash
flutter pub add dio
# flutter pub add dio_cookie_manager
# flutter pub add cookie_jar
```

> `dio_cookie_manager` `cookie_jar` 这两个我暂时没用上

### 第 2 步：常量定义

lib/common/values/constants.dart

```dart
/// 常量
class Constants {
  // wp 服务器
  static const wpApiBaseUrl = 'https://wpapi.ducafecat.tech';

```

### 第 3 步：单例初始

lib/common/services/wp_http.dart

```dart
import 'dart:io';

import 'package:dio/dio.dart';
import 'package:get/get.dart' hide Response, FormData, MultipartFile;

import '../index.dart';

class WPHttpService extends GetxService {
  static WPHttpService get to => Get.find();

  late final Dio _dio;
  // final CancelToken _cancelToken = CancelToken(); // 默认去掉

  @override
  void onInit() {
    super.onInit();

    // 初始 dio
    var options = BaseOptions(
      baseUrl: Constants.wpApiBaseUrl,
      connectTimeout: 10000, // 10秒
      receiveTimeout: 5000, // 5秒
      headers: {},
      contentType: 'application/json; charset=utf-8',
      responseType: ResponseType.json,
    );
    _dio = Dio(options);

    // 拦截器
    _dio.interceptors.add(RequestInterceptors());
  }

}
```

### 第 4 步：方法 get/post/put/delete

lib/common/services/wp_http.dart

```dart
  Future<Response> get(
    String url, {
    Map<String, dynamic>? params,
    Options? options,
    CancelToken? cancelToken,
  }) async {
    Options requestOptions = options ?? Options();
    Response response = await _dio.get(
      url,
      queryParameters: params,
      options: requestOptions,
      cancelToken: cancelToken,
    );
    return response;
  }

  Future<Response> post(
    String url, {
    dynamic data,
    Options? options,
    CancelToken? cancelToken,
  }) async {
    var requestOptions = options ?? Options();
    Response response = await _dio.post(
      url,
      data: data ?? {},
      options: requestOptions,
      cancelToken: cancelToken,
    );
    return response;
  }

  Future<Response> put(
    String url, {
    dynamic data,
    Options? options,
    CancelToken? cancelToken,
  }) async {
    var requestOptions = options ?? Options();
    Response response = await _dio.put(
      url,
      data: data ?? {},
      options: requestOptions,
      cancelToken: cancelToken,
    );
    return response;
  }

  Future<Response> delete(
    String url, {
    dynamic data,
    Options? options,
    CancelToken? cancelToken,
  }) async {
    var requestOptions = options ?? Options();
    Response response = await _dio.delete(
      url,
      data: data ?? {},
      options: requestOptions,
      cancelToken: cancelToken,
    );
    return response;
  }
```

### 第 5 步：错误拦截处理

lib/common/services/wp_http.dart

```dart

/// 拦截
class RequestInterceptors extends Interceptor {
  @override
  void onRequest(RequestOptions options, RequestInterceptorHandler handler) {
    // super.onRequest(options, handler);
    // if (UserService.to.hasToken) {
    //   options.headers['Authorization'] = 'Bearer ${UserService.to.token}';
    // }
    return handler.next(options);
    // 如果你想完成请求并返回一些自定义数据，你可以resolve一个Response对象 `handler.resolve(response)`。
    // 这样请求将会被终止，上层then会被调用，then中返回的数据将是你的自定义response.
    //
    // 如果你想终止请求并触发一个错误,你可以返回一个`DioError`对象,如`handler.reject(error)`，
    // 这样请求将被中止并触发异常，上层catchError会被调用。
  }

  @override
  void onResponse(Response response, ResponseInterceptorHandler handler) {
    // 200 请求成功, 201 添加成功
    if (response.statusCode != 200 && response.statusCode != 201) {
      handler.reject(
        DioError(
          requestOptions: response.requestOptions,
          response: response,
          type: DioErrorType.response,
        ),
        true,
      );
    } else {
      handler.next(response);
    }
  }

  /// 退出并重新登录
  // Future<void> _errorNoAuthLogout() async {
  //   await UserService.to.logout();
  //   Get.toNamed(RouteNames.systemLogin);
  // }

  @override
  Future<void> onError(DioError err, ErrorInterceptorHandler handler) async {
    final exception = HttpException(err.message);
    switch (err.type) {
      case DioErrorType.response: // 服务端自定义错误体处理
        {
          // final response = err.response;
          // final errorMessage = ErrorMessageModel.fromJson(response?.data);
          // switch (errorMessage.statusCode) {
          //   case 401:
          //     _errorNoAuthLogout();
          //     break;
          //   case 404:
          //     break;
          //   case 500:
          //     break;
          //   case 502:
          //     break;
          //   default:
          //     break;
          // }
          // Loading.error(errorMessage.message);
        }
        break;
      case DioErrorType.other:
        break;
      case DioErrorType.cancel:
        break;
      case DioErrorType.connectTimeout:
        break;
      default:
        break;
    }
    err.error = exception;
    handler.next(err);
  }
}
```

### 最后 Global 载入

lib/global.dart

```dart
class Global {
  static Future<void> init() async {
    WidgetsBinding widgetsBinding = WidgetsFlutterBinding.ensureInitialized();
    ...

    // 初始化服务
    ...
    Get.put<WPHttpService>(WPHttpService());
```

> 提交代码到 git
