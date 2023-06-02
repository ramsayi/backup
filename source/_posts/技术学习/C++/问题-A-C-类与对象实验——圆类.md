---
title: '问题 A: C++类与对象实验——圆类'
tags:
  - 4月25号12节
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: f48c336e
date: 2018-01-01 08:00:00
---

## 题目描述

设计一个圆形类Circle，要求数据成员为私有，成员函数为公有，成员函数至少要包含构造函数，负责输入的input()，负责求周长的perimeter()函数，负责求面积的area()函数，负责输出结论的output()函数。注意，求得的周长和面积都在output()函数中输出。主函数中定义对象，通过调用input()、perimeter()、area()和output()函数，完成输入一个半径，分别输出周长和面积。说明：圆周率（π）取3.14。

## 输入

一个浮点数，代表半径值。

## 输出

圆的周长和面积，结果保留两位小数且各占一行，行尾输出换行。

## 样例输入

```
2.5
```

## 样例输出

```
15.70
19.62
```

## 提示

```c++
#include<iostream>
using namespace std;
class Circle {
		const float PI = 3.14;
		float r, l, s;
	public:
		Circle() {}
		void input() {
			cin >> r;
		}
		void perimeter() {
			l = 2 * PI * r;
		}
		void area() {
			s = PI * r * r;
		}
		void output() {
			cout.precision(2);
			cout << fixed << l << endl << fixed << s << endl;
		}
};
int main() {
	Circle obj;
	obj.input();
	obj.perimeter();
	obj.area();
	obj.output();
	return 0;
}
```

