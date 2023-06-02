---
title: '问题 A: C++类的继承——学生类'
tags:
  - 5月6号78节
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: 1a350f0a
date: 2018-01-01 08:00:00
---

## 题目描述

Student类含有私有数据成员:num,name,sex，公有成员函数: 输入函数get_value()和输出函数display()。采用公用继承方式实现类Student1，增加数据成员:age,addr，成员函数:get_value_1()和display_1()。在程序运行时输入num,name,sex,age,addr的值，调用输出函数输出以上5个数据的值。

## 输入

输入num,name,sex,age,addr的值

## 输出

输入num,name,sex,age,addr的值

## 样例输入

```
1001 zhang m 21 shanghai
```

## 样例输出

```
num: 1001
name: zhang
sex: m
age: 21
address: shanghai
```

## 提示

```c++
#include<iostream>
using namespace std;
class Student{
	int num;
	string name,sex;
public:
	void get_value(){
		cin>>num>>name>>sex;
	}
	void display(){
		cout<<"num: "<<num<<endl;
		cout<<"name: "<<name<<endl;
		cout<<"sex: "<<sex<<endl;
	}
};
class Student1:public Student{
	int age;
	string addr;
public:
	void get_value_1(){
		cin>>age>>addr;
	}
	void display_1(){
		cout<<"age: "<<age<<endl;
		cout<<"address: "<<addr<<endl;
	}
};
int main(){
	Student1 b;
	b.get_value();
	b.get_value_1();
	b.display();
	b.display_1();
	return 0;
}
```

