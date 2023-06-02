---
title: 'Error: listen EACCES: permission denied 0.0.0.0:80端口被占用'
tags:
  - 端口占用
categories:
  - 踩坑记录
  - 终端
abbrlink: 6cf75909
date: 2022-05-22 14:41:15
cover:
---

# 报错如下

![image-20220522145952247](/assets/img/article/image-20220522145952247.png)

# 端口被系统模块占用

`win+R` 打开 `cmd` 页面，输入 `netstat -ano | findstr 80` 命令查看 80端口被占用情况，如下图：

![image-20220522144538301](/assets/img/article/image-20220522144538301.png)

端口被 4 占用，查询发现 4 是 SYSTEM 模块，故在 cmd 页面再输入 `netsh http show servicestate` 查看 http 服务状态，发现请求队列如下：

![image-20220522144807030](/assets/img/article/image-20220522144807030.png)

在任务浏览器状态栏右键， 打开 PID 视图，找到 PID 序号为 4964的进程，右键结束进程即可释放 80 端口（图内已关闭 4964）

![image-20220522144849903](/assets/img/article/image-20220522144849903.png)
