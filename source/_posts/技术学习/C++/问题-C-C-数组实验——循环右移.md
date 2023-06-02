---
title: '问题 C: C++数组实验——循环右移'
tags:
  - 4月1号78节
categories:
  - 技术学习
  - C++
abbrlink: 448a4ec5
date: 2018-01-01 00:00:00
cover: /assets/img/post/c++.webp
---

## 题目描述

输入一个正整数n，定义一个包含n个元素的动态一维数组a（int型），键盘依次输入n个元素。将数组中的元素循环右移，即：a[0]移到a[1]，a[1移到a[2]，……，a[n-1] 移到a[0]。然后输出数组各元素。

## 输入



输入：元素个数n以及这n个元素





## 输出

输出：重新存放的n个元素（各元素之间有一个空格）

## 样例输入

```
8
1 3 5 7 2 4 6 9
```

## 样例输出

```
9 1 3 5 7 2 4 6
```

## 提示

```c++
#include<iostream>
using namespace std;
int main() {
	int n,x;
	cin>>n;
	int a[n];
	for(int i=0;i<n;i++)
		cin>>a[i];
	x=a[n-1];
	for(int i=n;i>0;i--)
		a[i]=a[i-1];
	a[0]=x;
	for(int i=0;i<n;i++)
		cout<<a[i]<<' ';
}
```

