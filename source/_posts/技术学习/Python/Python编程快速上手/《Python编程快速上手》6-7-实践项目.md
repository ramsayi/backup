---
title: 《Python编程快速上手》6.7 实践项目
tags:
  - Python
categories:
  - 技术学习
  - Python
  - Python编程快速上手
abbrlink: d9852e2d
cover: /assets/img/post/Python.webp
date: 2022-01-22 21:20:51
---

#### 表格打印

###### printTable 1

```python
tableData = [['apples', 'oranges', 'cherries', 'banana'],
             ['Alice', 'Bob', 'Carol', 'David'],
             ['dogs', 'cats', 'moose', 'goose']]

def printTable(data):
    colWidths = [0] * len(data)
    for b in range(len(data[0])):
        for a in range(len(data)):
            if colWidths[a] < len(data[a][b]):
                colWidths[a] = len(data[a][b])
    print(colWidths)

    for b in range(len(data[0])):
        for a in range(len(data)):
            if a == 0:
                print(data[a][b].rjust(colWidths[a]), end = ' ')
            else:
                print(data[a][b].ljust(colWidths[a]), end = ' ')
        print()

printTable(tableData)
```

###### 输出

```shell
[8, 5, 5]
  apples Alice dogs  
 oranges Bob   cats  
cherries Carol moose 
  banana David goose 
```



###### printTable 2

```python
def printTable(table):
    colWidths = [0] * len(table)
    lines = len(table)  # 3行
    cols = len(table[0])    # 4列
    for i in range(lines):  # 遍历列表3行
        col_max_len = 0
        for j in range(cols):   # 遍历列表4列
            if len(table[i][j]) > col_max_len:
                col_max_len = len(table[i][j])
        colWidths[i] = col_max_len
    for j in range(cols):   # 输出4行
        for i in range(lines):  # 输出3列
            print(table[i][j].rjust(colWidths[i]), end=' ')
        print('')


tableData = [['apple', 'orange', 'cherries', 'banana'],
             ['Alice', 'Bob', 'Carol', 'David'],
             ['dogs', 'cats', 'moose', 'goose']]

printTable(tableData)
```

###### 输出

```shell
   apple Alice  dogs 
  orange   Bob  cats 
cherries Carol moose 
  banana David goose 
```

