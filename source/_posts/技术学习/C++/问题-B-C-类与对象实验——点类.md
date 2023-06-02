---
title: '问题 B: C++类与对象实验——点类'
tags:
  - 4月25号12节
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: aa3c288f
date: 2018-01-01 08:00:00
---

## 题目描述

设有一描述坐标点的类Point，其私有变量x和y代表一个点的(x,y)坐标值。请编写程序实现以下功能：利用构造函数传递参数，在定义对象时将x、y坐标值初始化为（60,80）；利用公有成员函数void setPoint(int i, int j)将坐标值修改为(60+i,80+j)；利用公有成员函数display()输出修改后的坐标值。主函数中通过定义对象，验证各个函数。

## 输入

两个正整数，中间用空格隔开，代表用于修改点坐标的偏移量。

## 输出

修改后的点坐标，两个正整数，中间用空格隔开，行尾输出换行。

## 样例输入

```
3 5
```

## 样例输出

```
63 85
```

## 提示

```c++
#include<iostream>
using namespace std;
class Point {
		int x, y;
	public:
		Point(int xx = 60, int yy = 80) {
			x = xx;
			y = yy;
		}
		void setPoint(int i, int j) {
			x += i;
			y += j;
		}
		void display() {
			cout << x << ' ' << y << endl;
		}
};
int main() {
	int a, b;
	cin >> a >> b;
	Point obj;
	obj.setPoint(a, b);
	obj.display();
	return 0;
}
```

