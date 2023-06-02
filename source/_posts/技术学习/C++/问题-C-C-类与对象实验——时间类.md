---
title: '问题 C: C++类与对象实验——时间类'
tags:
  - 4月25号12节
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: ddd39f3e
date: 2018-01-01 08:00:00
---

## 题目描述

设计一个时间类Time，要求数据成员为私有，成员函数为公有，实现计算两个时刻的时间差（按秒计算）。

## 输入

共有两行，每行三个正整数，中间用空格隔开，代表两个时刻。

## 输出

一个正整数，即两个时刻的时间差，行尾输出换行。

## 样例输入

```
9 45 30
15 20 5
```

## 样例输出

```
20075
```

## 提示

```c++
#include<iostream>
using namespace std;
class Time {
		int hh, mm, ss, t;
		int hh2, mm2, ss2, t2;
		int difftime;
	public:
		void input() {
			cin >> hh >> mm >> ss;
			cin >> hh2 >> mm2 >> ss2;
		}
		void difftimes() {
			t = hh * 3600 + mm * 60 + ss;
			t2 = hh2 * 3600 + mm2 * 60 + ss2;
			if (t2 > t) {
				difftime = t2 - t;
			} else {
				difftime = t - t2;
			}
		}
		void output() {
			cout << difftime << endl;
		}
};
int main() {
	Time obj;
	obj.input();
	obj.difftimes();
	obj.output();
	return 0;
}
```

