---
title: '问题 C: C++类与对象——长方形类'
tags:
  - 4月29号78节
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: d388acaa
date: 2018-01-01 08:00:00
---

## 题目描述

定义长方形类rectangle，数据成员包括长length和宽width，均为double类型，成员函数包括： 

(1)构造函数2个，一个无参的构造函数，长和宽的默认值为0，带两个参数的构造函数;

(2)设置长方形尺寸函数assign，即任意输入2个实数，大的数赋值给长，小的数赋值给宽

(3)计算长方形周长函数double circumference();

(4)计算长方形面积的函数double area();

(5)输出长方形的长和宽

要求在main函数中创建3个长方形的对象，第1，2个长方形分别由无参构造函数和有参构造函数初始化实现，第3个长方形对象通过输入数据，调用设置长方形尺寸函数，给长宽赋值，然后分别计算3个长方形的周长和面积，并输出结果

## 输入

输入仅一行数据，输入2个实数，数据之间用空格分开

## 输出

3个长方形输出3行数据，每行数据先输出长方形的长、宽，再输出它对应的周长和面积，小数点后保留2位数字，一行中4个数据之间用逗号分隔

## 样例输入

```
2.5 3.8
```

## 样例输出

```
0.00,0.00,0.00,0.00
2.00,1.00,6.00,2.00
3.80,2.50,12.60,9.50
```

## 提示

```c++
#include<iostream>   
using namespace std;
class rectangle{
    double length,width;
    double x,y;
    public:
    	rectangle(){
            length=0;
            width=0;
        }
        rectangle(double a,double b){
            if(a>b) length=a,width=b;
            else length=b,width=a;
        }
        void assign(){
            cin>>x>>y;
            if(x>y) length=x,width=y;
            else length=y,width=x;
        }
        double circumference(){
            return (length+width)*2;
        }
        double area(){
            return length*width;
        }
        void lenwid(){
            cout.precision(2);
            cout<<fixed<<length<<','<<width<<',';
        }
};
int main(){
    rectangle m,n(2,1),p;
    p.assign();
    m.lenwid();
    cout<<m.circumference()<<','<<m.area()<<endl;
    n.lenwid();
    cout<<n.circumference()<<','<<n.area()<<endl;
    p.lenwid();
    cout<<p.circumference()<<','<<p.area()<<endl;
    return 0;
}
```

