---
title: '问题 B: C++类与对象——日期类'
tags:
  - 4月29号78节
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: 4ba28477
date: 2018-01-01 08:00:00
---

## 题目描述

设计一个日期类Date，要求数据成员为私有，成员函数为公有，其中setDate()用来设置日期，Rise()用来实现日期增加一天，Print()用来输出日期等。设计一个友元函数Equal()用来比较两个日期是否相等。主函数内定义相关对象，验证各个函数。

## 输入

共有两行，每行三个正整数，中间用空格隔开，代表两个日期。其中三个正整数分别对应年、月、日。

## 输出

共有三行，第一行输出两个日期是否相等的结果，相等输出True，不等输出False。第二行输出三个正整数，中间用空格隔开，代表第一个日期增加一天后的结果。第三行输出三个正整数，中间用空格隔开，代表第二个日期增加一天后的结果。三个正整数依次代表年、月、日，每行结尾输出换行。

## 样例输入

```
2000 2 28
1996 3 31
```

## 样例输出

```
False
2000 2 29
1996 4 1
```

## 提示

```c++
#include<iostream>
using namespace std;
class Date{
    int y,m,d;
    int days[12]={31,28,31,30,31,30,31,31,30,31,30,31};
    public:
    	void setDate(){
            cin>>y>>m>>d;
        }
        void Rise(){
            if(y%4==0&&y%100!=0||y%400==0) days[1]=29;
            if(m==12&&days[m-1]==d) y++,m=1,d=1;
            else if(days[m-1]==d) m++,d=1;
            else d++;
        }
        void Print(){
            cout<<y<<' '<<m<<' '<<d<<endl;
        }
        friend void Equal(Date m,Date n);
};
void Equal(Date a,Date b){
    if(a.y==b.y&&a.m==b.m&&a.d==b.d) cout<<"True"<<endl;
    else cout<<"False"<<endl;
}
int main(){
    Date a,b;
    a.setDate();
    b.setDate();
    Equal(a,b);
    a.Rise();
    a.Print();
    b.Rise();
    b.Print();
    return 0;
}
```

