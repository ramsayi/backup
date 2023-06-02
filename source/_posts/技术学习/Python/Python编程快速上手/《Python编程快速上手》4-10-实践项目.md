---
title: 《Python编程快速上手》4.10 实践项目
tags:
  - Python
categories:
  - 技术学习
  - Python
  - Python编程快速上手
abbrlink: c8321fba
cover: /assets/img/post/Python.webp
date: 2022-01-22 22:18:55
---

### 4.10.1 逗号代码

```python
def strlist(listname):
    spam = listname[0]
    for i in range(1, len(listname) - 1):
        spam = spam + ', ' + str(listname[i])
    spam = spam + ' and ' + str(listname[len(listname) - 1])
    return spam

spam = ['apples', 'bananas', 'tofu', 'cats']
example = strlist(spam)
example
```

###### 输出

```shell
'apples, bananas, tofu and cats'
```

### 4.10.2 字符图网格

```python
grid = [['.', '.', '.', '.', '.', '.'],
        ['.', 'O', 'O', '.', '.', '.'],
        ['O', 'O', 'O', 'O', '.', '.'],
        ['O', 'O', 'O', 'O', 'O', '.'],
        ['.', 'O', 'O', 'O', 'O', 'O'],
        ['O', 'O', 'O', 'O', 'O', '.'],
        ['O', 'O', 'O', 'O', '.', '.'],
        ['.', 'O', 'O', '.', '.', '.'],
        ['.', '.', '.', '.', '.', '.']]

for a in range(6):
    for b in range(9):
        print(grid[b][a], end = '')
    print('\n')
```

###### 输出

```shell
..OO.OO..

.OOOOOOO.

.OOOOOOO.

..OOOOO..

...OOO...

....O....
```

