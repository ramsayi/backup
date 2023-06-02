---
title: '问题 B: C++继承与派生——矩形类'
tags:
  - 5月6号78节
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: dae7ff7b
date: 2018-01-01 08:00:00
---

## 题目描述

通过本题目的练习可以掌握继承与派生的概念，派生类的定义和使用方法，其中派生类构造函数的定义是重点。

要求定义一个基类Point，它有两个私有的float型数据成员X,Y;一个构造函数用于对数据成员初始化；有一个成员函数void Move(float xOff, float yOff)实现分别对X,Y值的改变，其中参数xOff和yOff分别代表偏移量。另外两个成员函数GetX() 、GetY()分别返回X和Y的值。

Rectangle类是基类Point的公有派生类。它增加了两个float型的私有数据成员W,H; 增加了两个成员函数float GetH() 、float GetW()分别返回W和H的值；并定义了自己的构造函数，实现对各个数据成员的初始化。

编写主函数main()根据以下的输入输出提示，完成整个程序。

## 输入

6个float型的数据，分别代表矩形的横坐标X、纵坐标Y、宽度W，高度H、横向偏移量的值、纵向偏移量的值；每个数据之间用一个空格间隔

## 输出

输出数据共有4个，每个数据之间用一个空格间隔。分别代表偏移以后的矩形的横坐标X、纵坐标Y、宽度W，高度H的值

## 样例输入

```
5 6 2 3 1 2
```

## 样例输出

```
6 8 2 3
```

## 提示

```c++
#include<iostream>
using namespace std;
class Point{
	float X,Y;
public:
	Point(){
		cin>>X>>Y;
	}
	void Move(float xOff, float yOff){
		X+=xOff,Y+=yOff;
	}
	float GetX(){
		return X;
	}
	float GetY(){
		return Y;
	}
};
class Rectangle:public Point{
	float W,H;
public:
	Rectangle(){
		cin>>W>>H;
	}
	float GetW(){
		return W;
	}
	float GetH(){
		return H;
	}
};
int main(){
	Rectangle a;
	int ox,oy;
	cin>>ox>>oy;
	a.Move(ox,oy);
	cout<<a.GetX()<<' '<<a.GetY()<<' '<<a.GetW()<<' '<<a.GetH()<<endl;
	return 0;
}
```

