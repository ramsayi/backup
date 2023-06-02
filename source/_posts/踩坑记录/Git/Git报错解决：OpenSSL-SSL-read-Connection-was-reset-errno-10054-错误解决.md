---
title: 'Git报错解决：OpenSSL SSL_read: Connection was reset, errno 10054 错误解决'
tags:
  - Git
categories:
  - 踩坑记录
  - Git
abbrlink: e5af059c
date: 2021-09-09 14:07:01
---

![](/assets/img/post/e5af059c/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202021-09-09%20140843.png)

> 首先，造成这个错误很有可能是网络不稳定，连接超时导致的，
> 如果再次尝试后依然报错，可以执行下面的命令。

### 打开Git命令页面，执行git命令脚本：修改设置，解除ssl验证

```bash
git config --global http.sslVerify "false"
```

![](/assets/img/post/e5af059c/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202021-09-09%20141614.png)

此时，再执行git操作即可。

## 全局代理

```bash
git config --global http.proxy http://127.0.0.1:7890

git config --global http.proxy http://127.0.0.1:7890
```

取消全局代理：

```bash
git config --global --unset http.proxy

git config --global --unset https.proxy
```

