---
title: 安装 Win11 + Ubuntu 双系统过程
tags:
  - Ubuntu
categories:
  - 踩坑记录
  - Linux
abbrlink: 7a25a720
copyright: false
cover: '/assets/img/post/ubuntu.webp'
date: 2021-09-10 23:58:53
---

很多时候，我们不得不用到Linux系统，而平时工作学习生活用Windows更多，而虚拟机的方式，对硬件利用效率比较低下，一般只适合临时尝鲜（但现在Win10已经可以在应用商店像应用一样直接安装Linux子系统，基本功能都有，可以满足基本需要，只是桌面图形化受限，详细可以参考[在Win10中安装Ubuntu](https://jingyan.baidu.com/article/ae97a64617a90bbbfd461d80.html)），

为了更高的使用效率以及折腾学习Linux系统，很多人还是需要安装Windows+Linux双系统。知名的Linux发行版包括Debian、CentOS、Arch、Ubuntu以及国产的[深度deepin](https://www.deepin.org/)等等，其中Ubuntu系统在普通用户群体中使用最为广泛，系统使用的相关教程也比较多。

不过许多读研的同学等群体，安装Linux也只是为了完成课程需要或者临时兴趣，以后也许并不想过多深入研究Linux，待完成学业也想完全删除Linux而完全不影响Windows系统，所以需要以"两系统互不影响+最简"的方式安装双系统，本文记录总结了关于Windows+Ubuntu双系统安装的心得、经验，可以帮助新手快速上手，少走一些弯路。

*推荐先快速浏览全文后，再根据需求按步骤安装系统*

## 制作 Ubuntu 系统安装 U盘

1. 下载 Ubuntu 安装镜像，建议下载 LTS 长期支持版：https://ubuntu.com/download/desktop
2. 使用 rufus，或者使用其他镜像制作软件，将 Ubuntu 系统拷至 U 盘里，具体方法百度搜索一堆。

## 前期磁盘准备

1. 在 Win10 中，鼠标右键选择 `计算机` --> `管理` --> `磁盘管理`
2. 选择你需要安装 Ubuntu 的磁盘，右键选择 `压缩卷`，压缩一个你需要的空间大小（如何你是想当成主力使用的话，建议至少 80G，不要分配盘符）
3. 打开 `设置` --> `系统` --> `电源和睡眠` --> `其他电源设置` --> `选择电源按钮的功能` --> `更改当前不可用的设置` --> `关闭启用快速启动的选项`（如果上述步骤没找到，可以百度搜索 Win10 关闭快速启动方法）

## 前期 BIOS 准备

1. 重启电脑，开机后立刻按 `F2` 进入 BIOS（请注意：不同品牌的电脑按键可能不一样，如果不是 F2 键，请自行搜索你的电脑的 BIOS 进入按键）
2. 找到 `Security` 选项，将 `Security Boot` 选项关闭
3. 找到 `Fast Boot` 选项并关闭

## 安装 Ubuntu

1. 关闭电脑，插上刚才制作好的 U 盘
2. 启动电脑，按 `F12`，选择 U 盘启动
3. 接着会出现 Ubuntu 界面，选择 `Install Ubuntu`（接下来安装过程不要拔掉 U 盘）
4. 前几步自定义就行，整个过程不要联网，如果出现 `安装更新和第三方软件` 选项，取消勾选
5. 接着最重要的一步，出现安装类型界面时，选择 `其他选项`，不要选择 `安装 Ubuntu，与 Windows Boot Manager 共存` 这个选项，有点坑

## 安装类型配置

1. 点击你分配的磁盘，选择加号，进行如下配置（容量大小可以自定义）：
   1. /boot
      1. 大小：300M
      2. 新分区的类型：逻辑分区
      3. 新分区的位置：空间起始位置
      4. 用于：EXT4 日志文件系统
      5. 挂载点：/boot
   2. /
      1. 大小：建议 50G 左右即可
      2. 新分区的类型：主分区
      3. 新分区的位置：空间起始位置
      4. 用于：EXT4 日志文件系统
      5. 挂载点：/
   3. /home（这个主要是个人文件夹）
      1. 大小：剩下的都给它，如果你之前压缩了 80G 空间的话，现在应该还剩 29G 左右，都分配给它就行了。这个是存放个人文件的地方
      2. 新分区的类型：逻辑分区
      3. 新分区的位置：空间起始位置
      4. 用于：EXT4 日志文件系统
      5. 挂载点：/home
2. 找到你刚才新建的类型为 /boot 的设备名，在 `安装启动引导器的设备` 选项中，选中它
3. 点击 `现在安装` ，点击 `继续`
4. 后面的步骤完全自定义即可，没有什么坑了

## 安装结束

安装完成之后，将提示重新启动电脑，这时选择重启。重启的时候记得拔掉 U 盘。如果你重启发现进入的还是 Windows 系统，进入 BIOS 将启动项改为 Ubuntu 即可。

## 联网问题

联想电脑安装 Ubuntu 之后可能无法连接无线网或者无法重启电脑，有可能是还未更新导致，只要更新一下一般就能解决（至少我试的几台联想电脑都是可行的）。

1. 首先进入 Ubuntu 桌面，打开终端输入：`sudo modprobe -r ideapad_laptop`
2. 此时 WiFi 就可用了，然后连接 WiFi
3. 在终端输入：`sudo apt update` 以及 `sudo apt upgrade`
4. 如果你的电脑有独显的话，打开 `软件和更新`，找到 `附加驱动`，选择对应的电脑驱动。完成后重启电脑就行了。

相关推荐文章：

[个人 Linux 软件清单及相关问题解决方案（Ubuntu18.04LTS）](https://www.cnblogs.com/zhangxiaochn/p/12423303.html)
[Ubuntu 常用快捷键](https://www.cnblogs.com/zhangxiaochn/p/12213199.html)
[Ubuntu18.04 安装后的配置及相关问题解决方案](https://www.cnblogs.com/zhangxiaochn/p/12212953.html)
[Ubuntu18.04LTS 美化（仿Mac）](https://www.cnblogs.com/zhangxiaochn/p/12212876.html)

> [Windows10+Ubuntu18.04双系统快速简单安装指北](https://regulus.cc/2019/10/05/Windows10+Ubuntu18.04%E5%8F%8C%E7%B3%BB%E7%BB%9F%E7%AE%80%E5%8D%95%E5%AE%89%E8%A3%85%E6%8C%87%E5%8C%97/)
>
> [安装 Win10 + Ubuntu 双系统过程](https://www.cnblogs.com/zhangxiaochn/p/13096507.html)
