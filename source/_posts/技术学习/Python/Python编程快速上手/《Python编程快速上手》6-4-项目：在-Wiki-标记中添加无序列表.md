---
title: 《Python编程快速上手》6.4 项目：在 Wiki 标记中添加无序列表
tags:
  - Python
categories:
  - 技术学习
  - Python
  - Python编程快速上手
abbrlink: 6bbdbdae
cover: /assets/img/post/Python.webp
date: 2022-01-22 21:38:57
---

###### bulletPointAdder.py - 在Wiki标记中添加无序列表

```python
#! python3
# bulletPointAdder.py - 在Wiki标记中添加无序列表
# 每行文字都在剪贴板中。

import pyperclip
text = pyperclip.paste()

# 分割行并添加星号
lines = text.split('\n')
for i in range(len(lines)): # 遍历“行”列表中的所有索引
    lines[i] = '* ' + lines[i] # 为“行”列表中的每个字符串添加星号
text = '\n'.join(lines)
pyperclip.copy(text)
```

###### 示例文本

```text
Lists of animals
Lists of aquarium life
Lists of biologists by author abbreviation
Lists of cultivars
```

###### 输出

```text
* Lists of animals
* Lists of aquarium life
* Lists of biologists by author abbreviation
* Lists of cultivars
```

