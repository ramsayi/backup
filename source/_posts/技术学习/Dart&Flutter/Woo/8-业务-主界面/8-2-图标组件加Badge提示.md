---
title: 8.2 图标组件加 Badge 提示
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: 4e45d887
date: 2022-10-31 11:03:07
---

# 8.2 图标组件加 Badge 提示

## 效果

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image_nikgGgp34r.png" alt="img" style="zoom:50%;" />

## 实现步骤：

---

### 第 1 步：输入接口

```dart
/// 图标组件
class IconWidget extends StatelessWidget {
  ...
  final String? badgeString; // Badge 文字
```

### 第 2 步：build 实现

```dart
  @override
  Widget build(BuildContext context) {
    ...

    // 文字、数字
    if (badgeString != null) {
      return Badge(
        badgeContent: Text(
          badgeString!,
          style: TextStyle(
            color: AppColors.onPrimary,
            fontSize: 9,
          ),
        ),
        position: BadgePosition.topEnd(top: -7, end: -8),
        elevation: 0,
        badgeColor: AppColors.primary,
        padding: const EdgeInsets.all(4.0),
        child: icon,
      );
    }
```

### 第 3 步：main 视图中加入

lib/pages/system/main/view.dart

```dart
  // 主视图
  Widget _buildView() {
    ...
					items: [
                NavigationItemModel(
                  label: LocaleKeys.tabBarHome.tr,
                  icon: AssetsSvgs.navHomeSvg,
                ),
                NavigationItemModel(
                  label: LocaleKeys.tabBarCart.tr,
                  icon: AssetsSvgs.navCartSvg,
                  count: 3, // 购物车数量
                ),
                NavigationItemModel(
                  label: LocaleKeys.tabBarMessage.tr,
                  icon: AssetsSvgs.navMessageSvg,
                  count: 9, // 新消息数量
                ),
                NavigationItemModel(
                  label: LocaleKeys.tabBarProfile.tr,
                  icon: AssetsSvgs.navProfileSvg,
                ),
              ],
```

> 后期可以用 obs 响应变量更新

> 提交代码到 git
