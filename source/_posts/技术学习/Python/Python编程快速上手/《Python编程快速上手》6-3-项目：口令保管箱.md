---
title: 《Python编程快速上手》6.3 项目：口令保管箱
tags:
  - Python
categories:
  - 技术学习
  - Python
  - Python编程快速上手
abbrlink: 621d6fb0
cover: /assets/img/post/Python.webp
date: 2022-01-22 21:26:21
---

###### pw.py 一个口令保管箱

```python
#   pw.py 一个口令保管箱
import pyperclip
import sys

PASSWORDS = {'email': 'asdfihejkagwbascarevoiwera',
             'blog': 'seruniobthopaesrbnesropt',
             'luggage': 'asDIUrvbyialestdbhajlsnt'}

if len(sys.argv) < 2:
    print('Usage: py pw.py [account] - copy account password')
    sys.exit()

account = sys.argv[1]
if account in PASSWORDS:
    pyperclip.copy(PASSWORDS[account])
    print('Password for ' + account + ' copied to clipboard.')
else:
    print('There is no account name called ' + account)
```

