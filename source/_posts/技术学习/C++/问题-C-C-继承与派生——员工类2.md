---
title: '问题 C: C++继承与派生——员工类2'
tags:
  - 5月6号78节
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: cbc34163
date: 2018-01-01 08:00:00
---

## 题目描述

要求定义一个基类Person，它有3个protected的数据成员：姓名name(char *类型)、性别 sex(char类型)、年龄age(int类型)；一个构造函数用于对数据成员初始化；有一个成员函数show()用于输出数据成员的信息。

创建Person类的公有派生类Employee，增加两个数据成员 基本工资 basicSalary（int类型） 请假天数leaveDays（int型）；为它定义初始化成员信息的构造函数，和显示数据成员信息的成员函数show()。

## 输入

共5个数据，分别代表姓名、性别、年龄、基本工资、请假天数。

## 输出

如示例数据所示，共5行，分别代表姓名、年龄、性别、基本工资、请假天数

## 样例输入

```
zhangsan m 30 4000 2
```

## 样例输出

```
name:zhangsan
age:30
sex:m
basicSalary:4000
leavedays:2
```

## 提示

```c++
#include<iostream>
using namespace std;
class Persion{
protected:
	char*name;
	char sex;
	int age;
public:
	Persion(char*n,char s,int a){
		name=n,sex=s,age=a;
	}
	void show(){
		cout<<"name:"<<name<<endl;
		cout<<"age:"<<age<<endl;
		cout<<"sex:"<<sex<<endl;
	}
};
class Employee:public Persion{
	int sal,day;
public:
	Employee(char*n,char s,int a,int b,int l):Persion(n,s,a){
		sal=b,day=l;
	}
	void show(){
		cout<<"basicSalary:"<<sal<<endl;
		cout<<"leavedays:"<<day<<endl;
	}
};
int main(){
	char name[100],sex;
	int age,sal,day;
	cin>>name>>sex>>age>>sal>>day;
	Employee a(name,sex,age,sal,day);
	a.Persion::show();
	a.show();
	return 0;
}
```

