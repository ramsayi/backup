---
title: 联想拯救者R9000P安装Ubuntu后屏幕亮度无法调节解决方案
tags:
  - Ubuntu
categories:
  - 踩坑记录
  - Linux
abbrlink: d8b4433f
copyright: false
cover: '/assets/img/post/r9000p.webp'
date: 2021-09-11 09:04:00
---

联想拯救者使用Ryzen7处理器，显卡为AMD Radeon+nvidia Geforce RTX, 在Ubuntu20.04上安装后会有屏幕亮度过高且无法调节的问题，屏幕亮到刺眼，严重影响使用。

安装Brightness Controller可以实现对屏幕亮度的调节，但是每次开机后都要运行一下Brightness Controller才能获得较低的亮度，比较麻烦。另外，还存在Ubuntu启动过程中屏幕出现花屏的问题。

这两个问题都可以通过以下方案一并解决。

其实，上述两个问题都是由于Nvidia显卡驱动加载慢，结果被fbdev vga 驱动抢先加载导致的。

## **解决方法：**

## **1. 编辑/etc/initramfs-tools/modules：**

```bash
sudo gedit /etc/initramfs-tools/modules
```

添加以下内容：

```text
nvidia
nvidia-drm
nvidia-modeset
```

## **2. 更新initrd：**

```bash
sudo update-initramfs -u
```

## 3. 修改grub

```bash
sudo gedit /etc/default/grub
```

在文本编辑器中将原来的“GRUB_CMDLINE_LINUX="" ”，修改为：

```text
GRUB_CMDLINE_LINUX="acpi_backlight=vendor"
```

保存文件，退出文本编辑器。

## 4. 更新grub：

```bash
sudo update-grub
```

## 5. 添加Nvidia显卡背光设备设置：

```bash
sudo gedit /usr/share/X11/xorg.conf.d/10-nvidia.conf
```

## 6. 添加以下内容以激活亮度控制选项：

```text
Section "Device"
Identifier "Device0"
Driver "nvidia"
VendorName "NVIDIA Corporation"
Option "RegistryDwords" "EnableBrightnessControl=1"
Option "NoLogo" "True"
EndSection
```

## 7. 禁止ideapad_laptop驱动加载：

```bash
sudo gedit /etc/modprobe.d/blacklist.conf
```

通过文本编辑器中，在文件末尾添加：

```text
blacklist ideapad_laptop
```

保存后退出。

## 8. 配置systemd-backlight服务

配置文件位于/var/lib/systemd/backlight 目录下，检查是否有pci-0000:01:00.0:backlight:nvidia_0 这个文件，没有的话创建一个，

通过以下命令在文件pci-0000:01:00.0:backlight:nvidia_0中输入亮度值50：

```bash
echo 50|sudo tee pci-0000:01:00.0:backlight:nvidia_0
```

## 9.显卡切换为混合模式

重启时快速按`F2`进bios，把显卡连接方式切换为混合模式。

完成上述配置后重启电脑，屏幕按设置值配置了亮度，问题解决。

> [联想拯救者R7000安装Ubuntu20.04后屏幕亮度调节终极解决方案](https://zhuanlan.zhihu.com/p/348624522)
