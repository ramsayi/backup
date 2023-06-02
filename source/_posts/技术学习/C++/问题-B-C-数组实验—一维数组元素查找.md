---
title: '问题 B: C++数组实验—一维数组元素查找'
tags:
  - 4月1号78节
categories:
  - 技术学习
  - C++
abbrlink: f857272c
date: 2018-01-01 00:00:00
cover: /assets/img/post/c++.webp
---

## 题目描述



定义包含10个整型数的一维数组，从键盘输入10个整数，然后再输入一个待查找的整数x，判断如果能在数组中找到x，则输出x“ is found at ”、下标，否则输出x“ is not found”。



说明：如果数组中找到多个与x相同的数，则只输出找到的首个元素。



## 输入



输入：第1行输入10个整数



第2行输入1个待查找的整数



## 输出



输出：x “ is found at”、下标（数据之间空1格）



或者：输出 x“ is not found”



## 样例输入

```
23 14 45 26 90 85 67 48 62 65
85
```

## 样例输出

```
85 is found at 5
```

## 提示

```c++
#include<iostream>
using namespace std;
int main() {
	int arr[10],x,isFound=0;
	for(int i=0; i<10; i++)
		cin>>arr[i];
	cin>>x;

	for(int i=0; i<10; i++) {
		if(x==arr[i]) {
			cout<<x<<" is found at "<<i<<endl;
			isFound=1;
		}
	}
	if(isFound==0)
		cout<<x<<" is not found"<<endl;
}
```

