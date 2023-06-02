---
title: 《Python编程快速上手》7.18 实践项目
tags:
  - Python
categories:
  - 技术学习
  - Python
  - Python编程快速上手
abbrlink: a8f15a08
cover: /assets/img/post/Python.webp
date: 2022-01-24 14:23:00
---

### 7.18.1 强口令检测

写一个函数，它使用正则表达式，确保传入的口令字符串是强口令。

强口令的定义是：长度不少于 8 个字符，同时包含大写和小写字符，至少有一位数字。

你可能需要用多个正则表达式来测试该字符串，以保证它的强度。

```python
import re

def strong(str):
    m1 = re.search(r'\d', str)        # 至少有一位数字
    m2 = re.search(r'[A-Z]', str)    # 包含大写字符
    m3 = re.search(r'[a-z]+', str)    # 包含小写字符
    m4 = re.search(r'(.*){8,}', str)  # 长度不少于8个字符

    if m1 and m2 and m3 and m4:
        print('强密码')
    else:
        print('弱密码')

strong(input('请输入密码'))
```

### 7.18.2 strip()的正则表达式版本

写一个函数，它接受一个字符串，做的事情和 strip()字符串方法一样。

如果只传入了要去除的字符串，没有其他参数，那么就从该字符串首尾去除空白字符。

否则，函数第二个参数指定的字符将从该字符串中去除。

```python
import re

def stripRe():
    text = input("请输入文本：")
    word = input("请输入去除的字符串，默认空格则直接按'Enter键'")
    if word == '':
        stripRegex = re.compile(r'([a-zA-Z0-0])+(.*)*([a-zA-Z0-9])+')
        print(stripRegex.search(text).group())
    else:
        stripRegex = re.compile(f'{word}')
        print(stripRegex.sub('',text))

stripRe()
```

