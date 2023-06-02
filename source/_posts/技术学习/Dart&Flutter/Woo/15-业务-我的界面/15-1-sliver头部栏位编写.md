---
title: 15.1 sliver 头部栏位编写
tags:
  - Dart
  - Flutter
categories:
  - 技术学习
  - Dart&Flutter
  - Woo
cover: /assets/img/post/flutter.webp
abbrlink: 491beba8
date: 2022-10-31 11:03:07
---

# 15.1 sliver 头部栏位编写

<img src="https://ducafecat.oss-cn-beijing.aliyuncs.com/podcast/image-20220803083152336.png" alt="image-20220803083152336" style="zoom: 50%;" />

## 实现步骤：

---

### 第 1 步：i18n

lib/common/i18n/locale_keys.dart

```dart
  static const myTabWishlist = "my_tab_wishlist";
  static const myTabFollowing = "my_tab_following";
  static const myTabVoucher = "my_tab_voucher";
  static const myBtnMyOrder = "my_btn_my_order";
  static const myBtnMyWallet = "my_btn_my_wallet";
  static const myBtnEditProfile = "my_btn_edit_profile";
  static const myBtnAddress = "my_btn_address";
  static const myBtnNotification = "my_btn_notification";
  static const myBtnLanguage = "my_btn_language";
  static const myBtnTheme = "my_btn_theme";
  static const myBtnWinGift = "my_btn_win_gift";
  static const myBtnStyles = "my_btn_styles";
  static const myBtnLogout = "my_btn_logout";
  static const myBtnBillingAddress = "my_btn_billing_address";
  static const myBtnShippingAddress = "my_btn_shipping_address";
```

lib/common/i18n/locales/locale_en.dart

```dart
  // 我的
  LocaleKeys.myTabWishlist: 'Wishlist',
  LocaleKeys.myTabFollowing: 'Following',
  LocaleKeys.myTabVoucher: 'Voucher',
  LocaleKeys.myBtnMyOrder: 'My Order',
  LocaleKeys.myBtnMyWallet: 'My Wallet',
  LocaleKeys.myBtnEditProfile: 'Edit Profile',
  LocaleKeys.myBtnAddress: 'Address',
  LocaleKeys.myBtnNotification: 'Notification',
  LocaleKeys.myBtnLanguage: 'Language',
  LocaleKeys.myBtnTheme: 'Theme',
  LocaleKeys.myBtnWinGift: 'Win Gift',
  LocaleKeys.myBtnLogout: 'Logout',
  LocaleKeys.myBtnStyles: 'Styles',
  LocaleKeys.myBtnBillingAddress: 'Billing address',
  LocaleKeys.myBtnShippingAddress: 'Shipping address',
```

lib/common/i18n/locales/locale_zh.dart

```dart
  // 我的
  LocaleKeys.myTabWishlist: '喜欢',
  LocaleKeys.myTabFollowing: '关注',
  LocaleKeys.myTabVoucher: '收据',
  LocaleKeys.myBtnMyOrder: '我的订单',
  LocaleKeys.myBtnMyWallet: '我的钱包',
  LocaleKeys.myBtnEditProfile: '编辑个人资料',
  LocaleKeys.myBtnAddress: '送货地址',
  LocaleKeys.myBtnNotification: '消息',
  LocaleKeys.myBtnLanguage: '语言',
  LocaleKeys.myBtnTheme: '主题',
  LocaleKeys.myBtnWinGift: '赢取礼物',
  LocaleKeys.myBtnStyles: '样式组件',
  LocaleKeys.myBtnLogout: '注销',
  LocaleKeys.myBtnBillingAddress: '发票地址',
  LocaleKeys.myBtnShippingAddress: '配送地址',
```

### 第 2 步：验证登录

lib/pages/system/main/controller.dart

```dart
  // 切换页面
  void onJumpToPage(int page) {
    if ((page != 0) && !UserService.to.isLogin) {
      Get.toNamed(RouteNames.systemLogin);
    } else {
      pageController.jumpToPage(page);
    }
  }
```

### 第 3 步：导航栏按钮项

lib/pages/my/my_index/widgets/bar_item.dart

```dart
import 'package:flutter/material.dart';
import 'package:flutter_screenutil/flutter_screenutil.dart';
import 'package:flutter_woo_commerce_getx_learn/common/index.dart';

/// 功能栏项
class BarItemWidget extends StatelessWidget {
  final String title;
  final String svgPath;

  const BarItemWidget({
    Key? key,
    required this.title,
    required this.svgPath,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return <Widget>[
      // 图标
      IconWidget.svg(
        svgPath,
        size: 24.sp,
        color: AppColors.primary,
      ).paddingBottom(AppSpace.iconTextSmail),

      // 标题
      TextWidget.body2(
        title,
      ),
    ].toColumn();
  }
}

```

### 第 4 步：顶部 APP 导航栏

lib/pages/my/my_index/view.dart

```dart
  // 顶部 APP 导航栏
  Widget _buildAppBar() {
    return SliverAppBar(
      // 背景色
      backgroundColor: Colors.transparent,
      // 固定在顶部
      pinned: true,
      // 浮动在顶部
      floating: true,
      // 自动弹性显示
      snap: true,
      // 是否应拉伸以填充过度滚动区域。
      stretch: true,
      // 高度
      expandedHeight: 280.h,
      // 此小组件堆叠在工具栏和选项卡栏后面。其高度将与应用栏的整体高度相同。
      flexibleSpace: FlexibleSpaceBar(
        // // 折叠模式
        // collapseMode: CollapseMode.parallax,
        // // 折叠动画
        // stretchModes: const [
        //   // 模糊
        //   StretchMode.blurBackground,
        //   // 尺寸
        //   StretchMode.zoomBackground,
        //   // 标题动画
        //   StretchMode.fadeTitle,
        // ],
        // 标题
        // title: const TextWidget.navigation(text: "Ducafecat"),
        // 背景
        background: <Widget>[
          // 背景图
          <Widget>[
            IconWidget.svg(
              AssetsSvgs.profileHeaderBackgroundSvg,
              color: AppColors.primaryContainer,
              fit: BoxFit.cover,
            ).expanded(),
            // const ImageWidget.(
            //   AssetsImages.profileBackgroundPng,
            //   fit: BoxFit.cover,
            // ).expanded(),
          ].toColumn(
            crossAxisAlignment: CrossAxisAlignment.stretch,
          ),

          // 内容
          <Widget>[
            // 用户信息
            <Widget>[
              // 头像
              ImageWidget.url(
                // 测试需要改成自定义头像
                "https://ducafecat.oss-cn-beijing.aliyuncs.com/avatar/00258VC3ly1gty0r05zh2j60ut0u0tce02.jpg",
                width: 100.w,
                height: 100.w,
                fit: BoxFit.fill,
                radius: 50.w,
              ).paddingRight(AppSpace.listItem),

              // 称呼
              TextWidget.title1(
                "${UserService.to.profile.username}",
                color: AppColors.primary,
                size: 26.sp,
              ),
            ].toRow().paddingHorizontal(AppSpace.card),

            // 功能栏位
            <Widget>[
              // 1
              BarItemWidget(
                title: LocaleKeys.myTabWishlist.tr,
                svgPath: AssetsSvgs.iLikeSvg,
              ),
              // 2
              BarItemWidget(
                title: LocaleKeys.myTabFollowing.tr,
                svgPath: AssetsSvgs.iAddFriendSvg,
              ),
              // 3
              BarItemWidget(
                title: LocaleKeys.myTabVoucher.tr,
                svgPath: AssetsSvgs.iCouponSvg,
              ),
            ]
                .toRow(
                  mainAxisAlignment: MainAxisAlignment.spaceAround,
                )
                .paddingAll(AppSpace.card)
                .card()
                .paddingHorizontal(AppSpace.page),
          ].toColumn(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          ),
        ].toStack(),
      ),
    );
  }
```

### 第 5 步：视图

lib/pages/my/my_index/view.dart

```dart
  // My Order
  Widget _buildMyOrder() {
    return Text("My Order");
  }

  // 按钮列表
  Widget _buildButtonsList() {
    return Text("按钮列表");
  }
```

```dart
  // 主视图
  Widget _buildView() {
    return CustomScrollView(
      slivers: <Widget>[
        // 顶部 APP 导航栏
        _buildAppBar(),
        // My Order
        _buildMyOrder().sliverBox,
        // 按钮列表
        _buildButtonsList().sliverBox,

        // 注销
        ButtonWidget.primary(
          LocaleKeys.myBtnLogout.tr,
          height: 60,
        )
            .padding(
              left: AppSpace.page,
              right: AppSpace.page,
              bottom: AppSpace.listRow * 2,
            )
            .sliverBox,

        // 版权
        const TextWidget.body2(
          "Code by: https://ducafefcat.tech",
        ).alignCenter().paddingBottom(AppSpace.listRow).sliverBox,

        // 版本号
        TextWidget.body2(
          "v ${ConfigService.to.version}",
        ).alignCenter().paddingBottom(200).sliverBox,
      ],
    );
  }
```

```dart
  @override
  Widget build(BuildContext context) {
    return GetBuilder<MyIndexController>(
      init: MyIndexController(),
      id: "my_index",
      builder: (_) {
        return Scaffold(
          body: _buildView(),
        );
      },
    );
  }
```

> 提交代码到 git
