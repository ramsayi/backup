---
title: '问题 C: C++综合练习——键盘'
tags:
  - C++理论综合作业
categories:
  - 技术学习
  - C++
cover: '/assets/img/post/c++.webp'
abbrlink: 1761ca15
date: 2018-01-01 08:00:00
---

## 题目描述

假如你的键盘上坏了几个键，那么在敲一段文字的时候，对应的字符就不会出现。现在给出应该输入的一段文字、以及实际被输入的文字，请你列出肯定坏掉的那些键。

## 输入

输入在 2 行中分别给出应该输入的文字、以及实际被输入的文字。每段文字是不超过 80 个字符的串，由字母 A-Z（包括大、小写）、数字 0-9、以及下划线_（代表空格）组成。题目保证 2 个字符串均非空。

## 输出

按照发现顺序，在一行中输出坏掉的键。其中英文字母只输出大写，每个坏键只输出一次。题目保证至少有 1 个坏键。

## 样例输入

```
7_This_is_a_test
_hs_s_a_es
```

## 样例输出

```
7TI
```

## 提示

```c++
#include<iostream>
#include<string>
using namespace std;
int main(){
	string s1,s2,s,a;
	cin>>s1>>s2;
	for(int i=0,j=0;i<s1.size();i++,j++)
		if(s1[i]!=s2[j]){
		if(s1[i]>='a'&&s1[i]<='z') a=s1[i]-32;
		else a=s1[i];
		if(s.find(a)==-1) s.append(a);
		j--;
	}
	cout<<s<<endl;
	return 0;
}

```

