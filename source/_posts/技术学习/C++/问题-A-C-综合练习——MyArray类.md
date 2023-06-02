---
title: '问题 A: C++综合练习——MyArray类'
tags:
  - C++理论综合作业
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: 8fd81083
date: 2018-01-01 08:00:00
---

## 题目描述

设计一个MyArray类，用来模拟一个由小到大的有序的整数序列，实现输入一个整数，将其插入序列，并保持该序列由小到大有序。MyArray类原型如下：

class MyArray

{private:

int a[50];  //存储一个由小到大有序的整数序列

int n;   //记录序列中数据的个数

public:

MyArray(int x) { n=x; }  //初始化，通过x的值确定序列的大小

void input();  //从键盘输入n个由小到大有序的整数

void insert(int k); //将k值按由小到大的顺序插入到序列中(注意，插入一个数据后，n值要增一)

void output();  //输出序列中的数据

};

## 输入

第一行有一个正整数n，表示原始的整数序列长度为n，保证n不超过50。

第二行有n个整数，表示原始的整数序列，保证这个序列是从小到大给出的。

第三行有一个整数，表示需要插入的整数。

## 输出

在一行中输出n+1个整数，表示完成插入的整数序列。每个整数后输出一个空格。请注意行尾输出换行。

## 样例输入

```
10
1 2 3 4 5 6 7 9 10 11
8
```

## 样例输出

```
1 2 3 4 5 6 7 8 9 10 11
```

## 提示

```c++
#include<iostream>
using namespace std;
class MyArray {
	private:
		int a[50];  //存储一个由小到大有序的整数序列
		int n;    //记录序列中数据的个数
	public:
		MyArray(int x) {
			n = x;    //初始化，通过x的值确定序列的大小
		}
		void input();  //从键盘输入n个由小到大有序的整数
		void insert(int k); //将k值按由小到大的顺序插入到序列中(注意，插入一个数据后，n值要增一)
		void output();  //输出序列中的数据
};
void MyArray::input() {
	for (int i = 0; i < n; i++) {
		cin >> a[i];
	}
}
void MyArray::insert(int k) {
	int i = 0;
	while (k > a[i]) i++;
	for (int j = n; j >= i; j--) a[j + 1] = a[j];
	a[i] = k;
	n++;
}
void MyArray::output() {
	for (int i = 0; i < n; i++) cout << a[i] << ' ';
}
int main() {
	int x, k;
	cin >> x;
	MyArray arr(x);
	arr.input();
	cin >> k;
	arr.insert(k);
	arr.output();
	return 0;
}
```

