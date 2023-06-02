---
title: 'Git: pull时提示Please commit your changes or stash them before you merge.'
tags:
  - Git
categories:
  - 踩坑记录
  - Git
cover: '/assets/img/post/git.webp'
abbrlink: 3a5d5839
date: 2022-05-05 19:18:28
---

对本地的代码进行修改后，直接git pull会提示本地代码和github代码冲突，需要先commit本地代码，或者stash他们

解决方法分两种情况：

1. 希望保留本地的修改，pull之后，修改依然存在

```bash
git stash
git pull 
git stash pop 
```

解析：
git stash: 将改动藏起来
git pull:用新代码覆盖本地代码
git stash pop: 将刚藏起来的改动恢复
这样操作的效果是在最新的仓库代码的基础仍保留本地的改动

1. 不保留本地的修改，直接覆盖

```bash
git reset --hard
git pull 
```
