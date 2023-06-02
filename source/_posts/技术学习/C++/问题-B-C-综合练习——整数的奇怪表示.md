---
title: '问题 B: C++综合练习——整数的奇怪表示'
tags:
  - C++理论综合作业
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: 2aae77a2
date: 2018-01-01 08:00:00
---

## 题目描述

假如用字母 H 来表示“百”、字母 T 表示“十”，用 12...n 来表示不为零的个位数字 n（<10），换个格式来输出任一个不超过 3 位的正整数。例如 234 应该被输出为 HHTTT1234，因为它有 2 个“百”、3 个“十”、以及个位的 4。

## 输入

每个测试输入包含 1 个测试用例，给出正整数 n（<1000）。

## 输出

每个测试用例的输出占一行，用规定的格式输出 n。

## 样例输入

```
232
```

## 样例输出

```
HHTTT12
```

## 提示

```c++
#include<iostream>
using namespace std;
int main(){
	int x,a,b,c;
	cin>>x;
	c=x%10;
	b=x/10%10;
	a=x/100%10;
	while(a--) cout<<"H";
	while(b--) cout<<"T";
	for(int i=1;i<=c;i++) cout<<i;
	cout<<endl;
	return 0;
}
```

