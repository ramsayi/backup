---
title: '问题 B: 求N以内的素数'
tags:
  - 4月22号78节
categories:
  - 技术学习
  - C++
abbrlink: fea9501a
date: 2018-01-01 00:00:00
cover: /assets/img/post/c++.webp
---

## 题目描述

求N以内（包括N）的素数。(N<=100000)

## 输入

N

## 输出

N以内的所有素数，一个素数占一行。

## 样例输入

```
100
```

## 样例输出

```
2
3
5
7
11
13
17
19
23
29
31
37
41
43
47
53
59
61
67
71
73
79
83
89
97
```

## 提示

```c++
#include<iostream>
#include<cmath>
using namespace std;
void outPrime(int a){
	int i,j;
	for(i=2;i<=a;i++){
		for(j=2;j<=sqrt(i);j++)
			if(i%j==0) break;
		if(j>sqrt(i))
			cout<<i<<endl;
	}
}
int main(){
	int n;
	cin>>n;
	outPrime(n);
	return 0;
}
```

