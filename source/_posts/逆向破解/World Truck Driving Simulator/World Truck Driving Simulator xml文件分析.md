---
title: 世界卡车 解锁全部车辆 代码分析
tags:
  - 游戏
  - 世界卡车模拟
categories:
  - 逆向破解
  - World Truck Driving Simulator
abbrlink: b2c596f5
date: 2020-02-22 14:30:04
---

# 车辆对应xml代码 已注释

```xml
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>

<map>
    <!-- 金币 -->
    <!-- 初始金币 = EDEJARYBVkVZDwIArmZAEA%3D%3D -->
    <!-- 100100100.00金币 = GjEJCxwAXF5TAlgbDwIAchSy8w%3D%3D -->
    <!-- 正无穷 = EDsECxYBXFFZDwIAI7dfPQ%3D%3D -->
    <string name="EW1DUxQ%3D">GjEJCxwAXF5TAlgbDwIAchSy8w%3D%3D</string>


    <!-- 等级 -->
    <!-- 30级 = %2F9V1ZQUCADY%2BRos%3D -->
    <string name="C31I">%2F9V1ZQUCADY%2BRos%3D</string>
    
    <!-- 默认打开目录为存储卡根目录 -->
    <string name="OxOD.lastPath">%2Fstorage%2Femulated%2F0%2F</string>


​    

    <!-- Resolution 分辨率 -->
    <!-- Height 高度 -->
    <!-- 50% = 540 -->
    <!-- 75% = 810 -->
    <!-- 100% = 1080 -->
    <int name="Screenmanager%20Resolution%20Height" value="1080" />
    <!-- Width 宽度 -->
    <!-- 50% = 1080 -->
    <!-- 75% = 1620 -->
    <!-- 100% = 2160 -->
    <int name="Screenmanager%20Resolution%20Width" value="2160" />
    
    <!-- Quality 画质 -->
    <!-- Very Low = 0 -->
    <!-- Normal = 1 -->
    <!-- High = 2 -->
    <int name="UnityGraphicsQuality" value="2" />
    <int name="nQuali" value="2" />
    
    <!-- Shadows 阴影 -->
    <!-- Off = 0 -->
    <!-- On = 1 -->
    <int name="nShadow" value="1" />
    
    <!-- Bushes/Grass 灌木/草丛 -->
    <!-- Off = 0 -->
    <!-- On = 1 -->
    <int name="sMatos" value="1" />
    
    <!-- Visual Effects 视觉效果 -->
    <!-- Off = 0 -->
    <!-- On = 1 -->
    <int name="vEffects" value="1" />
    
    <!-- Choose your preferred Visual Effect 选择您喜欢的视觉效果 -->
    <!-- 0, 1, 2, 3, 4 -->
    <int name="mEfeito" value="1" />
    
    <!-- Controls 控制 -->
    <!-- Tilt = 1 -->
    <!-- Arrows = 2 -->
    <!-- Whell = 3 -->
    <!-- Gamepad = 4 -->
    <int name="nContr" value="1" />
    
    <!-- Sensitivity 灵敏度 -->
    <!-- Tilt
    <!-- 0.1 - 0.12345678 - 1.0 -->
    <float name="mSensibTilt" value="0.5" />
    
    <!-- Sensitivity 灵敏度 -->
    <!-- Arrows
    <!-- 0.1 - 0.12345678 - 1.0 -->
    <float name="mSensibSeta" value="0.5" />
    <!-- Steer Release Speed 转向释放速度 -->
    <!-- 0.05 - 0.12345678 - 1.0 -->
    <float name="mSensibSoltSeta" value="0.5" />
    
    <!-- Sensitivity 灵敏度 -->
    <!-- Whell
    <!-- 0.1 - 0.12345678 - 0.8 -->
    <float name="mSensibVol" value="0.5" />
    <!-- Steer Release Speed 转向释放速度 -->
    <!-- 0.1 - 0.12345678 - 1.0 -->
    <float name="mSensibSolt" value="0.5" />
    
    <!-- Sensitivity 灵敏度 -->
    <!-- Gamepad
    <!-- 0.1 - 0.12345678 - 1.0 -->
    <float name="mSensibJoy" value="0.1" />
    
    <!-- Pedal Type 踏板类型 -->
    <!-- 滑块 = 0 -->
    <!-- 按钮 = 1 -->
    <int name="mTipoPedal" value="1" />
    
    <!-- Traffic 交通 -->
    <!-- Off = 0 -->
    <!-- Low = 1 -->
    <!-- Medium = 2 -->
    <!-- High = 3 -->
    <!-- Very High = 4 -->
    <int name="nTraf" value="1" />
    
    <!-- Left Mirror 左后视镜 -->
    <!-- On Screen = 0 -->
    <!-- On Vehicle = 1 -->
    <int name="retroEsq" value="1" />
    
    <!-- Right Mirror 右后视镜 -->
    <!-- On Screen = 0 -->
    <!-- On Vehicle = 1 -->
    <int name="retroDir" value="0" />
    
    <!-- Gear 档位 -->
    <!-- Automatic = 0 -->
    <!-- Manual = 1 -->
    <int name="sManual" value="0" />
    
    <!-- Cargo Damage 货物损坏 -->
    <!-- Off = 0 -->
    <!-- On = 1 -->
    <int name="mStatusDanos" value="1" />
    
    <!-- Language 语言 -->
    <!-- Portuguese = Por -->
    <!-- English = Ing -->
    <!-- Spanish = Esp -->
    <string name="mLinguagem">Ing</string>
    
    <!-- Sound 声音 -->
    <!-- Off = 0 -->
    <!-- On = 1 -->
    <int name="nSoun" value="1" />


​    

    <!-- 1 大众 Constellation -->
    <string name="Bgg%3D">YiMCADH3kjg%3D</string>
    
    <!-- 2 依维柯 Hi-Way -->
    <string name="Bgk%3D">YiMCADH3kjg%3D</string>
    
    <!-- 3 斯堪尼亚 T113 -->
    <string name="Bgo%3D">YiMCADH3kjg%3D</string>
    
    <!-- 4 斯堪尼亚 113 Frontal -->
    <string name="Bgs%3D">YiMCADH3kjg%3D</string>
    
    <!-- 5 斯堪尼亚 T124 -->
    <string name="Bgw%3D">YiMCADH3kjg%3D</string>
    
    <!-- 6 斯堪尼亚 P310 -->
    <string name="Bg0%3D">YiMCADH3kjg%3D</string>
    
    <!-- 7 斯堪尼亚 S730 -->
    <string name="Bg4%3D">YiMCADH3kjg%3D</string>
    
    <!-- 8 沃尔沃 VM -->
    <string name="Bg8%3D">YiMCADH3kjg%3D</string>
    
    <!-- 9 沃尔沃 FH16 750 -->
    <string name="BgA%3D">YiMCADH3kjg%3D</string>
    
    <!-- 10 奔驰 Axor -->
    <string name="BgE%3D">YiMCADH3kjg%3D</string>
    
    <!-- 11 依维柯 Hi-Way -->
    <string name="BgkA">YiMCADH3kjg%3D</string>
    
    <!-- 12 彼得比尔特 359 -->
    <string name="BgkB">YiMCADH3kjg%3D</string>
    
    <!-- 13 斯堪尼亚 T113 -->
    <string name="BgkC">YiMCADH3kjg%3D</string>
    
    <!-- 14 斯堪尼亚 113 Frontal -->
    <string name="BgkD">YiMCADH3kjg%3D</string>
    
    <!-- 15 斯堪尼亚 T124 -->
    <string name="BgkE">YiMCADH3kjg%3D</string>
    
    <!-- 16 斯堪尼亚 S730 -->
    <string name="BgkF">YiMCADH3kjg%3D</string>
    
    <!-- 17 沃尔沃 FH16 750 -->
    <string name="BgkG">YiMCADH3kjg%3D</string>
    
    <!-- 18 沃尔沃 FH09 -->
    <string name="BgkH">YiMCADH3kjg%3D</string>
    
    <!-- 19 斯堪尼亚 S730 -->
    <string name="BgkI">YiMCADH3kjg%3D</string>
    
    <!-- 20 沃尔沃 FH16 750 -->
    <string name="BgkJ">YiMCADH3kjg%3D</string>
    
    <!-- 21 沃尔沃 FH09 -->
    <string name="BgoA">YiMCADH3kjg%3D</string>
    
    <!-- 22 大众 Constellation 平板 -->
    <string name="BgoB">YiMCADH3kjg%3D</string>
    
    <!-- 23 大众 Constellation 货箱 -->
    <string name="BgoC">YiMCADH3kjg%3D</string>
    
    <!-- 24 斯堪尼亚 P310 货箱 -->
    <string name="BgoD">YiMCADH3kjg%3D</string>
    
    <!-- 25 斯堪尼亚 P310 平板 -->
    <string name="BgoE">YiMCADH3kjg%3D</string>
    
    <!-- 26 沃尔沃 VM 平板 -->
    <string name="BgoF">YiMCADH3kjg%3D</string>
    
    <!-- 27 沃尔沃 VM 货箱 -->
    <string name="BgoG">YiMCADH3kjg%3D</string>
    
    <!-- 28 大众 Constellation 4×8 货箱 -->
    <string name="BgoH">YiMCADH3kjg%3D</string>
    
    <!-- 29 大众 Constellation 4×8 平板 -->
    <string name="BgoI">YiMCADH3kjg%3D</string>
    
    <!-- 30 斯堪尼亚 P310 4×8 货箱 -->
    <string name="BgoJ">YiMCADH3kjg%3D</string>
    
    <!-- 31 斯堪尼亚 P310 4×8 平板 -->
    <string name="BgsA">YiMCADH3kjg%3D</string>
    
    <!-- 32 沃尔沃 VM 4×8 货箱 -->
    <string name="BgsB">YiMCADH3kjg%3D</string>
    
    <!-- 33 沃尔沃 VM 4×8 平板 -->
    <string name="BgsC">YiMCADH3kjg%3D</string>
    
    <!-- 34 奔驰 1620 -->
    <string name="BgsD">YiMCADH3kjg%3D</string>
    
    <!-- 35 斯堪尼亚 R620 -->
    <string name="BgsE">YiMCADH3kjg%3D</string>
    
    <!-- 36 斯堪尼亚 R620 -->
    <string name="BgsF">YiMCADH3kjg%3D</string>
    
    <!-- 37 奔驰 1113-1313 -->
    <string name="BgsG">YiMCADH3kjg%3D</string>
    
    <!-- 38 肯沃斯 K100 -->
    <string name="BgsH">YiMCADH3kjg%3D</string>
    
    <!-- 39 奔驰 Atego -->
    <string name="BgsI">YiMCADH3kjg%3D</string>
    
    <!-- 40 奔驰 Atego -->
    <string name="BgsJ">YiMCADH3kjg%3D</string>
    
    <!-- 41 奔驰 Atego 4×8 -->
    <string name="BgwA">YiMCADH3kjg%3D</string>
    
    <!-- 42 奔驰 New Actros -->
    <string name="BgwB">YiMCADH3kjg%3D</string>
    
    <!-- 43 奔驰 New Actros -->
    <string name="BgwC">YiMCADH3kjg%3D</string>
    
    <!-- 44 沃尔沃 FMX -->
    <string name="BgwD">YiMCADH3kjg%3D</string>
    
    <!-- 45 彼得比尔特 386 -->
    <string name="BgwE">YiMCADH3kjg%3D</string>
    
    <!-- 46 福特 -->
    <string name="BgwF">YiMCADH3kjg%3D</string>
    
    <!-- 47 福特 -->
    <string name="BgwG">YiMCADH3kjg%3D</string>
    
    <!-- 48 沃尔沃 VNL 860 -->
    <string name="BgwH">YiMCADH3kjg%3D</string>
    
    <!-- 49 大众 VW Titan -->
    <string name="BgwI">YiMCADH3kjg%3D</string>
    
    <!-- 50 MAN TGX-->
    <string name="BgwJ">YiMCADH3kjg%3D</string>
    
    <!-- 52 大众 VW Titan -->
    <string name="Bg0A">YiMCADH3kjg%3D</string>
    
    <!-- 53 斯堪尼亚 111 -->
    <string name="Bg0B">YiMCADH3kjg%3D</string>
    
    <!-- 54 福莱纳 -->
    <string name="Bg0C">YiMCADH3kjg%3D</string>
    
    <!-- 55 沃尔沃 NL12 EDC -->
    <string name="Bg0D">YiMCADH3kjg%3D</string>
    
    <!-- 56 沃尔沃 NL12 EDC -->
    <string name="Bg0E">YiMCADH3kjg%3D</string>
    
    <!-- 57 马克 -->
    <string name="Bg0F">YiMCADH3kjg%3D</string>
    
    <!-- 58 未知 -->
    <string name="Bg0G">YiMCADH3kjg%3D</string>
    
    <!-- 59 未知 -->
    <string name="Bg0H">YiMCADH3kjg%3D</string>
    
    <!-- 60 未知 -->
    <string name="Bg0I">YiMCADH3kjg%3D</string>
    
    <!-- 61 未知 -->
    <string name="Bg0J">YiMCADH3kjg%3D</string>
    
    <!-- 未知 -->
    <string name="BgaA">YiMCADH3kjg%3D</string>
    <string name="BgbA">YiMCADH3kjg%3D</string>
    <string name="BgcA">YiMCADH3kjg%3D</string>
    <string name="BgdA">YiMCADH3kjg%3D</string>
    <string name="BgeA">YiMCADH3kjg%3D</string>
    <string name="BgfA">YiMCADH3kjg%3D</string>
    <string name="BggA">YiMCADH3kjg%3D</string>
    <string name="BghA">YiMCADH3kjg%3D</string>
    <string name="BgiA">YiMCADH3kjg%3D</string>
    <string name="BgjA">YiMCADH3kjg%3D</string>
    <!-- <string name="BgkA">YiMCADH3kjg%3D</string> -->
    <string name="BglA">YiMCADH3kjg%3D</string>
    <string name="BgmA">YiMCADH3kjg%3D</string>
    <string name="BgnA">YiMCADH3kjg%3D</string>
    <!-- <string name="BgoA">YiMCADH3kjg%3D</string> -->
    <string name="BgpA">YiMCADH3kjg%3D</string>
    <string name="BgqA">YiMCADH3kjg%3D</string>
    <string name="BgrA">YiMCADH3kjg%3D</string>
    <!-- <string name="BgsA">YiMCADH3kjg%3D</string> -->
    <string name="BgtA">YiMCADH3kjg%3D</string>
    <string name="BguA">YiMCADH3kjg%3D</string>
    <string name="BgvA">YiMCADH3kjg%3D</string>
    <!-- <string name="BgwA">YiMCADH3kjg%3D</string> -->
    <string name="BgxA">YiMCADH3kjg%3D</string>
    <string name="BgyA">YiMCADH3kjg%3D</string>
    <string name="BgzA">YiMCADH3kjg%3D</string>

</map>
```



# 代码文件

```xml
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<map>
    <string name="EW1DUxQ%3D">GjEJCxwAXF5TAlgbDwIAchSy8w%3D%3D</string>
    <string name="C31I">%2F9V1ZQUCADY%2BRos%3D</string>
    <string name="OxOD.lastPath">%2Fstorage%2Femulated%2F0%2F</string>
    <int name="Screenmanager%20Resolution%20Height" value="1080" />
    <int name="Screenmanager%20Resolution%20Width" value="2160" />
    <int name="UnityGraphicsQuality" value="2" />
    <int name="nQuali" value="2" />
    <int name="nShadow" value="1" />
    <int name="sMatos" value="1" />
    <int name="vEffects" value="1" />
    <int name="mEfeito" value="1" />
    <int name="nContr" value="1" />
    <float name="mSensibTilt" value="0.5" />
    <float name="mSensibSeta" value="0.5" />
    <float name="mSensibSoltSeta" value="0.5" />
    <float name="mSensibVol" value="0.5" />
    <float name="mSensibSolt" value="0.5" />
    <float name="mSensibJoy" value="0.1" />
    <int name="mTipoPedal" value="1" />
    <int name="nTraf" value="1" />
    <int name="retroEsq" value="1" />
    <int name="retroDir" value="0" />
    <int name="sManual" value="0" />
    <int name="mStatusDanos" value="1" />
    <string name="mLinguagem">Ing</string>
    <int name="nSoun" value="1" />
    <string name="Bgg%3D">YiMCADH3kjg%3D</string>
    <string name="Bgk%3D">YiMCADH3kjg%3D</string>
    <string name="Bgo%3D">YiMCADH3kjg%3D</string>
    <string name="Bgs%3D">YiMCADH3kjg%3D</string>
    <string name="Bgw%3D">YiMCADH3kjg%3D</string>
    <string name="Bg0%3D">YiMCADH3kjg%3D</string>
    <string name="Bg4%3D">YiMCADH3kjg%3D</string>
    <string name="Bg8%3D">YiMCADH3kjg%3D</string>
    <string name="BgA%3D">YiMCADH3kjg%3D</string>
    <string name="BgE%3D">YiMCADH3kjg%3D</string>
    <string name="BgkA">YiMCADH3kjg%3D</string>
    <string name="BgkB">YiMCADH3kjg%3D</string>
    <string name="BgkC">YiMCADH3kjg%3D</string>
    <string name="BgkD">YiMCADH3kjg%3D</string>
    <string name="BgkE">YiMCADH3kjg%3D</string>
    <string name="BgkF">YiMCADH3kjg%3D</string>
    <string name="BgkG">YiMCADH3kjg%3D</string>
    <string name="BgkH">YiMCADH3kjg%3D</string>
    <string name="BgkI">YiMCADH3kjg%3D</string>
    <string name="BgkJ">YiMCADH3kjg%3D</string>
    <string name="BgoA">YiMCADH3kjg%3D</string>
    <string name="BgoB">YiMCADH3kjg%3D</string>
    <string name="BgoC">YiMCADH3kjg%3D</string>
    <string name="BgoD">YiMCADH3kjg%3D</string>
    <string name="BgoE">YiMCADH3kjg%3D</string>
    <string name="BgoF">YiMCADH3kjg%3D</string>
    <string name="BgoG">YiMCADH3kjg%3D</string>
    <string name="BgoH">YiMCADH3kjg%3D</string>
    <string name="BgoI">YiMCADH3kjg%3D</string>
    <string name="BgoJ">YiMCADH3kjg%3D</string>
    <string name="BgsA">YiMCADH3kjg%3D</string>
    <string name="BgsB">YiMCADH3kjg%3D</string>
    <string name="BgsC">YiMCADH3kjg%3D</string>
    <string name="BgsD">YiMCADH3kjg%3D</string>
    <string name="BgsE">YiMCADH3kjg%3D</string>
    <string name="BgsF">YiMCADH3kjg%3D</string>
    <string name="BgsG">YiMCADH3kjg%3D</string>
    <string name="BgsH">YiMCADH3kjg%3D</string>
    <string name="BgsI">YiMCADH3kjg%3D</string>
    <string name="BgsJ">YiMCADH3kjg%3D</string>
    <string name="BgwA">YiMCADH3kjg%3D</string>
    <string name="BgwB">YiMCADH3kjg%3D</string>
    <string name="BgwC">YiMCADH3kjg%3D</string>
    <string name="BgwD">YiMCADH3kjg%3D</string>
    <string name="BgwE">YiMCADH3kjg%3D</string>
    <string name="BgwF">YiMCADH3kjg%3D</string>
    <string name="BgwG">YiMCADH3kjg%3D</string>
    <string name="BgwH">YiMCADH3kjg%3D</string>
    <string name="BgwI">YiMCADH3kjg%3D</string>
    <string name="BgwJ">YiMCADH3kjg%3D</string>
    <string name="Bg0A">YiMCADH3kjg%3D</string>
    <string name="Bg0B">YiMCADH3kjg%3D</string>
    <string name="Bg0C">YiMCADH3kjg%3D</string>
    <string name="Bg0D">YiMCADH3kjg%3D</string>
    <string name="Bg0E">YiMCADH3kjg%3D</string>
    <string name="Bg0F">YiMCADH3kjg%3D</string>
</map>
```
