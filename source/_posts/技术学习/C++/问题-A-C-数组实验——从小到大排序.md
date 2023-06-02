---
title: '问题 A: C++数组实验——从小到大排序'
tags:
  - 4月1号78节
categories:
  - 技术学习
  - C++
abbrlink: f9b5041
date: 2018-01-01 00:00:00
cover: /assets/img/post/c++.webp
---

## 题目描述

输入一个正整数n，定义一个包含n个元素的动态一维数组（double型），输入n个元素，对这n个元素按照从小到大顺序排序，输出排序以后的各个元素。

## 输入



输入：元素个数n以及这n个元素



## 输出



输出：这n个元素按照从小到大顺序排序以后的结果（各元素之间有一个空格）



## 样例输入

```
5
3.2 1.4 8.5 4.6 2.2
```

## 样例输出

```
1.4 2.2 3.2 4.6 8.5
```

## 提示

```c++
#include<iostream>
using namespace std;
int main() {
	int n;
	cin>>n;
	double arr[n];
	for(int i=0; i<n; i++)
		cin>>arr[i];
	for(int i=0; i<n-1; i++) {
		for(int j=0; j<n-i-1; j++) {
			if(arr[j]>arr[j+1]) {
				double tmp = arr[j];
				arr[j] = arr[j+1];
				arr[j+1] = tmp;
			}
		}
	}
	for(int i=0;i<n;i++){
		cout<<arr[i]<<' ';
	}
}
```

