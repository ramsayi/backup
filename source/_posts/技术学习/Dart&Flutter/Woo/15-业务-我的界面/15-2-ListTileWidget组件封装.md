---
title: 15.2 ListTileWidget 组件封装
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: 491763c5
date: 2022-10-31 11:03:07
---

# 15.2 ListTileWidget 组件封装

## 实现步骤：

---

> 官方的 `ListTile` 虽然很方便，但是有两个主要问题
>
> 1. 不能改高度
> 2. 自定义能力还有点不足
>
> 所以我们项目中需要自己去实现一个 `ListTileWidget`

### 第 1 步：功能分析

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_dkCB_TsuKX.png" alt="img" style="zoom:50%;" />

功能：

1. 左右图标
2. 标题、子标题、描述
3. 尺寸、间距、边距
4. 事件、点击、长按

### 第 2 步：组件代码

lib/common/widgets/list_tile.dart

```dart
import 'package:flutter/material.dart';

import '../index.dart';

/// 列表行 ListTile 替代版本
class ListTileWidget extends StatelessWidget {
  /// 标题
  final Widget? title;

  /// 子标题
  final Widget? subtitle;

  /// 描述
  final Widget? description;

  /// 左侧图标
  final Widget? leading;

  /// 左侧图标间距
  final double? leadingSpace;

  /// 右侧图标
  final List<Widget>? trailing;

  /// padding 边框间距
  final EdgeInsetsGeometry? padding;

  /// cross 对齐方式
  final CrossAxisAlignment? crossAxisAlignment;

  /// 点击事件
  final GestureTapCallback? onTap;

  /// 长按事件
  final GestureLongPressCallback? onLongPress;

  ListTileWidget({
    Key? key,
    this.title,
    this.subtitle,
    this.description,
    this.leading,
    this.leadingSpace,
    this.trailing,
    EdgeInsetsGeometry? padding,
    this.crossAxisAlignment,
    this.onTap,
    this.onLongPress,
  })  : padding = padding ?? AppSpace.edgeInput,
        super(key: key);

  _buildView() {
    List<Widget> ws = [];

    // 头部图标
    if (leading != null) {
      ws.add(
        leading!.paddingRight(
          leadingSpace ?? AppSpace.iconTextSmail,
        ),
      );
    }

    // 标题/子标题/描述
    List<Widget> titles = [
      if (title != null) title!,
      if (subtitle != null) subtitle!,
      if (description != null) description!,
    ];
    MainAxisAlignment titleMainAxisAlignment = titles.length == 1
        ? MainAxisAlignment.center
        : MainAxisAlignment.spaceBetween;
    ws.add(
      titles
          .toColumn(
            mainAxisAlignment: titleMainAxisAlignment,
            crossAxisAlignment: CrossAxisAlignment.start,
          )
          .expanded(),
    );

    // 右侧图标
    if (trailing != null) {
      MainAxisAlignment trailingMainAxisAlignment = trailing?.length == 1
          ? MainAxisAlignment.center
          : MainAxisAlignment.spaceBetween;
      ws.add(
        trailing!.toColumn(
          mainAxisAlignment: trailingMainAxisAlignment,
        ),
      );
    }

    return ws
        .toRow(
          crossAxisAlignment: crossAxisAlignment ?? CrossAxisAlignment.center,
        )
        .backgroundColor(Colors.transparent)
        .padding(value: padding)
        .onTap(onTap)
        .onLongPress(onLongPress);
  }

  @override
  Widget build(BuildContext context) {
    return _buildView();
  }
}

```

> 提交代码到 git
