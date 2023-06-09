---
title: '问题 D: C++综合练习——身份证'
tags:
  - C++理论综合作业
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: 306ffe3
date: 2018-01-01 08:00:00
---

## 题目描述

一个合法的身份证号码由17位地区、日期编号和顺序编号加1位校验码组成。校验码的计算规则如下：

首先对前17位数字加权求和，权重分配为：{7，9，10，5，8，4，2，1，6，3，7，9，10，5，8，4，2}；然后将计算的和对11取模得到值Z；最后按照以下关系对应Z值与校验码M的值：

```
Z：0 1 2 3 4 5 6 7 8 9 10 
M：1 0 X 9 8 7 6 5 4 3 2 

	
```

现在给定一些身份证号码，请你验证校验码的有效性，并输出有问题的号码。

## 输入

输入第一行给出正整数N（≤100）是输入的身份证号码的个数。随后N行，每行给出1个18位身份证号码。

## 输出

按照输入的顺序每行输出1个有问题的身份证号码。这里并不检验前17位是否合理，只检查前17位是否全为数字且最后1位校验码计算准确。如果所有号码都正常，则输出All passed。

## 样例输入

```
4
320124198808240056
12010X198901011234
110108196711301866
37070419881216001X
```

## 样例输出

```
12010X198901011234
110108196711301866
37070419881216001X
```

## 提示

```c++
#include<iostream>
using namespace std;
int main(){
	int n,allpassed=0;
	cin>>n;
	char a[n][18];
	for(int i=0;i<n;i++)
		for(int j=0;j<18;j++)
			cin>>a[i][j];
	int q[17]={7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2};
	char m[11]={'1','0','X','9','8','7','6','5','4','3','2'};
	for(int i=0;i<n;i++){
		int x=0,notnum=0;
		for(int j=0;j<17;j++){
			if(!isdigit(a[i][j])){
				notnum=1;
				break;
			}
			x+=(a[i][j]-48)*q[j];
		}
		if(m[x%11]!=a[i][17]||notnum){
			for(int k=0;k<18;k++)
				cout<<a[i][k];
			cout<<endl;
		} else allpassed++;
	}
	if(allpassed==n)
		cout<<"All passed"<<endl;
	return 0;
}

```

