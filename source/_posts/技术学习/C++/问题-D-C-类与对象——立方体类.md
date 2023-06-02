---
title: '问题 D: C++类与对象——立方体类'
tags:
  - 4月29号78节
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: fec652e4
date: 2018-01-01 08:00:00
---

## 题目描述

编写基于对象的程序，求长方柱（Bulk）的体积。数据成员包括长（length）、宽（width）、高（heigth）、体积，要求用成员函数实现下面的功能：

（1）由键盘输入长方柱的长、宽、高；

（2）计算长方柱的体积（volume）和表面积（areas）；

（3）输出这长方柱的体积和表面积。

## 输入

长方柱的长、宽、高

## 输出

长方柱的体积和表面积

## 样例输入

```
2 3 4
```

## 样例输出

```
24
52
```

## 提示

```c++
#include<iostream>
using namespace std;
class Bulk{
    double length,width,heigth;
    public:
    	void input(){
            cin>>length>>width>>heigth;
        }
    	double volume(){
            return length*width*heigth;
        }
        double areas(){
            return 2*(length*width)+2*(width*heigth)+2*(length*heigth);
        }
};
int main(){
    Bulk a;
    a.input();
    cout<<a.volume()<<endl;
    cout<<a.areas()<<endl;
    return 0;
}
```

