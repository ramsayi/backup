---
title: Cmder启动报错
tags:
  - Cmder
  - 终端
categories:
  - 踩坑记录
  - 终端
abbrlink: 1f32a1d
date: 2021-08-27 22:45:15
---

[](https://i.loli.net/2021/08/27/qEavi5YAPerx41u.png)

#### 按照官方的FAQ设置MacType为独立启动模式并不能解决问题, 只好将ConEmuC添加到exclude list了 :

- 1.右键任务栏的MacType, 选择打开配置文件 -> 用记事本打开
- 2.找到UnloadDll
- 3.在其下添加相关进程

```
[UnloadDll]
ConEmuC.exe
ConEmuC64.exe
```

