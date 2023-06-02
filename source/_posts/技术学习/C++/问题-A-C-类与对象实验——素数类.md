---
title: '问题 A: C++类与对象实验——素数类'
tags:
  - 4月29号78节
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: 20b9268c
date: 2018-01-01 08:00:00
---

## 题目描述

设计一个素数类Prime，要求数据成员为私有，成员函数为公有，成员函数至少要包含构造函数，负责输入的input()，负责判断的judge()函数，负责输出结论的output()函数。主函数中定义对象，通过调用input()、judge()和output()函数，完成一个数是否为素数的判断。

## 输入

一个大于等于3并小于10000的正整数n。

## 输出

如果n是素数，输出“prime”，否则请输出“not prime”。

请注意不需要输出引号，行尾输出换行。

## 样例输入

```
29
```

## 样例输出

```
prime
```

## 提示

```c++
#include<iostream>
#include<cmath>
using namespace std;
class Prime{
    int n,i;
    bool a=false;
	public:
    	void input(){
        	cin>>n;
    	}
        void judge(){
            for(i=3;i<sqrt(n);i++)
            	if(n%i==0) break;
            if(i>sqrt(n)) a=true;
        }
        void output(){
            if(a) cout<<"prime"<<endl;
            else cout<<"not prime"<<endl;
        }
};
int main(){
    Prime a;
    a.input();
    a.judge();
    a.output();
    return 0;
}
```

