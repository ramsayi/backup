---
title: '问题 C: 奥运奖牌计数'
tags:
  - 4月22号78节
categories:
  - 技术学习
  - C++
abbrlink: 55b2a1a5
date: 2018-01-01 00:00:00
cover: /assets/img/post/c++.webp
---

## 题目描述

2008年北京奥运会，A国的运动员参与了n天的决赛项目(1≤n≤17)。现在要统计一下A国所获得的金、银、铜牌数目及总奖牌数。

## 输入

输入n＋1行，第1行是A国参与决赛项目的天数n，其后n行，每一行是该国某一天获得的金、银、铜牌数目，以一个空格分开。

## 输出

输出1行，包括4个整数，为A国所获得的金、银、铜牌总数及总奖牌数，以一个空格分开。

## 样例输入

```
3
1 0 3
3 1 0
0 3 0
```

## 样例输出

```
4 4 3 11
```

## 提示

```c++
#include<iostream>
using namespace std;
int main(){
	int x,gol(0),sil(0),cop(0),sum(0);
	cin>>x;
	int a[x][3];
	for(int i=0;i<x;i++)
		for(int j=0;j<3;j++)
			cin>>a[i][j];
	for(int i=0;i<x;i++){
		gol+=a[i][0];
		sil+=a[i][1];
		cop+=a[i][2];
	}
	sum=gol+sil+cop;
	cout<<gol<<' '<<sil<<' '<<cop<<' '<<sum<<endl;
	return 0;
}
```

