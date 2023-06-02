---
title: 解决Github图片不显示问题
tags:
  - Github
categories:
  - 踩坑记录
  - Github
abbrlink: 8e0faafe
date: 2021-05-29 13:33:19
---

以下为Windows10系统解决方案，其他系统暂未尝试。

主要思路为 修改DNS服务器的IP地址。

## 修改DNS服务器地址 

> 阿里云DNS服务器地址为`223.5.5.5`和 `223.6.6.6`**

### 1.打开网络和Internet设置
![](https://cdn.jsdelivr.net/gh/ramsayi/gallery/content/解决Github图片不显示问题/QQ截图20210710182118.png)

### 2.更改适配器选项

![](https://cdn.jsdelivr.net/gh/ramsayi/gallery/content/解决Github图片不显示问题/QQ截图20210710182758.png)

### 3.选择某个网络

这里选择当前正在使用的网络,wifi或者是宽带,我用的是宽带，双击打开

![](https://cdn.jsdelivr.net/gh/ramsayi/gallery/content/解决Github图片不显示问题/QQ截图20210710184316.png)

### 4.设置DNS

![](https://cdn.jsdelivr.net/gh/ramsayi/gallery/content/解决Github图片不显示问题/QQ截图20210710184501.png)

![](https://cdn.jsdelivr.net/gh/ramsayi/gallery/content/解决Github图片不显示问题/QQ截图20210710184631.png)

## 结果
![](https://cdn.jsdelivr.net/gh/ramsayi/gallery/content/解决Github图片不显示问题/QQ截图20210710185052.png)
