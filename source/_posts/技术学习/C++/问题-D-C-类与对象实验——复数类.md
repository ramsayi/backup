---
title: '问题 D: C++类与对象实验——复数类'
tags:
  - 4月25号12节
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: '73424431'
date: 2018-01-01 08:00:00
---

## 题目描述

定义一个复数类Complex，复数的实部real和虚部image定义为类的私有数据成员。成员函数均为公有，其中input()函数给实部和虚部赋值，output()函数按照“实部,虚部i”的格式输出复数，add()函数实现两个复数的相加。设计一个友元函数sub()实现两个复数的相减。主函数中定义若干对象，通过调用成员函数和友元函数，完成两个复数的相加和相减。

## 输入

共有两行，每行两个整数，中间用空格隔开，代表两个复数。其中，前一个数是实部，后一个数是虚部。

## 输出

共有两行，每行按照“实部,虚部i”的格式，逗号为英文逗号，不要输出引号。第一行是相加后的复数，第二行是相减后的复数，行尾输出换行。

## 样例输入

```
2 -1
3 1
```

## 样例输出

```
5,0i
-1,-2i
```

## 提示

```c++
#include<iostream>
#include<cmath>
using namespace std;
class Complex {
		int real, image;
		int real1, image1;
		int real2, image2;
	public:
		void input() {
			cin >> real >> image;
		}
		void output() {
			cout << real1 << ',' << image1 << 'i' << endl;
			cout << real2 << ',' << image2 << 'i' << endl;
		}
		void add(Complex m, Complex n);
		void sub(Complex m, Complex n);
};
void Complex::add(Complex m, Complex n) {
	real1 = m.real + n.real;
	image1 = m.image + n.image;
}
void Complex::sub(Complex m, Complex n) {
	real2 = m.real - n.real;
	image2 = m.image - n.image;
}
int main() {
	Complex m, n, p;
	m.input();
	n.input();
	p.add(m, n);
	p.sub(m, n);
	p.output();
	return 0;
}
```

