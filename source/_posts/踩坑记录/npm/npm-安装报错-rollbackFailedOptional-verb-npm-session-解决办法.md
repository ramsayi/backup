---
title: npm 安装报错 rollbackFailedOptional verb npm-session 解决办法
copyright: false
tags:
  - 终端
categories:
  - 踩坑记录
  - npm
abbrlink: 23ff30ca
date: 2021-08-22 20:53:55
---

## 简单分析

```powershell
root@ROYALHUANG-MB2:~/DevOps/elasticsearch/elasticsearch-head-master#     npm install -g grunt-cli
npm ERR! code ETIMEDOUT
npm ERR! errno ETIMEDOUT
npm ERR! network request to http://registry.npm.taobao.org/grunt-cli failed, reason: connect ETIMEDOUT 114.55.80.225:80
npm ERR! network This is a problem related to network connectivity.
npm ERR! network In most cases you are behind a proxy or have bad network settings.
npm ERR! network
npm ERR! network If you are behind a proxy, please make sure that the
npm ERR! network 'proxy' config is set properly.  See: 'npm help config'

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/ray/.npm/_logs/2018-08-09T07_35_44_967Z-debug.log
```

该问题是网络环境导致，解决方法分为两个方面

- npm代理和git代理都要设置（首先确认网络是否需要设置代理）

- 讲npm换为国内镜像cnpm，使用淘宝镜像作为下载资源

## 代理的修改与删除

### 如果是公司网络需要设置代理，则设置npm代理和git代理

1、设置npm代理

```powershell
npm config set proxy http://127.0.0.1:1080
```

```powershell
npm config set https-proxy http://127.0.0.1:1080
```

如果代理需要认证的话可以这样来设置

```powershell
npm config set proxy http://username:password@server:port
```

```powershell
npm config set https-proxy http://username:pawword@server:port
```

2、设置git代理

```powershell
git config --global http.proxy http://127.0.0.1:1080
```

```powershell
git config --global https.proxy https://127.0.0.1:1080
```

### 如果所用网络不需要代理，则要把npm代理和git代理去掉

1、去掉npm代理

```powershell
npm config delete proxy
```

```powershell
npm config delete https-proxy
```

2、去掉git代理

```powershell
git config --global --unset http.proxy
```

```powershell
git config --global --unset https.proxy
```

## 使用cnpm的获取镜像

1.安装cnpm

(1) 输入以下命令

```powershell
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

(2) 输入cnpm -v输入是否正常，这里肯定会出错。

```powershell
cnpm -v
```

(3) 添加系统变量path的内容

　　因为系统变量path并未包含该cnpm路径。在系统变量下添加该路径即可正常使用cnpm

附上环境变量配置方法：

> mac变量变量配置参考：https://blog.csdn.net/u010416101/article/details/54618621
>
> win系统配置：https://jingyan.baidu.com/article/00a07f3876cd0582d128dc55.html
>

 

## 修改npm的资源镜像链接

```powershell
npm config set registry http://registry.npm.taobao.org
```

> 版权声明：本文为CSDN博主「RoyalRay」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接：https://blog.csdn.net/qq_31945977/article/details/81537917
