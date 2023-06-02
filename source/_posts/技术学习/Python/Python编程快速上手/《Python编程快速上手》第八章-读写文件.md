---
title: 《Python编程快速上手》第八章 读写文件
tags:
  - Python
categories:
  - 技术学习
  - Python
  - Python编程快速上手
abbrlink: 5d67c4fe
cover: /assets/img/post/Python.webp
date: 2022-01-24 20:18:29
---

## 8.1 文件与文件路径

在 Windows 中，根文件夹名为 C:\，也称为 C：盘。

在 OS X 和 Linux 中，根文件夹是/。

### 8.1.1 Windows 上的倒斜杠以及 OS X 和 Linux 上的正斜杠

如果将单个文件和路径上的文件夹名称的字符串传递给它，`os.path.join()`就会返回一个文件路径的字符串，包含正确的路径分隔符。

```python
>>> import os
>>> os.path.join('usr', 'bin', 'spam')
'usr\\bin\\spam'
```

如果需要创建文件名称的字符串，`os.path.join()`函数就很有用。

```python
>>> myFiles = ['accounts.txt', 'details.csv', 'invite.docx']
>>> for filename in myFiles:
	print(os.path.join('C:\\Users\\asweigart', filename))
C:\Users\asweigart\accounts.txt
C:\Users\asweigart\details.csv
C:\Users\asweigart\invite.docx
```

### 8.1.2 当前工作目录

利用 `os.getcwd()`函数，可以取得当前工作路径的字符串，并可以利用 `os.chdir()`改变它。

```python
>>> import os
>>> os.getcwd()
'C:\\Python34'
>>> os.chdir('C:\\Windows\\System32')
>>> os.getcwd()
'C:\\Windows\\System32'
```

### 8.1.3 绝对路径与相对路径

• “绝对路径”，总是从根文件夹开始。

• “相对路径”，它相对于程序的当前工作目录。

单个的句点（`.`）用作文件夹目名称时，是“这个目录”的缩写。

两个句点（`..`）意思是父文件夹。

### 8.1.4 用 os.makedirs()创建新文件夹 

程序可以用 `os.makedirs()`函数创建新文件夹（目录）

```python
>>> import os
>>> os.makedirs('C:\\delicious\\walnut\\waffles')
```

### 8.1.5 os.path 模块

os.path 模块的完整文档在 Python 网站上：http://docs.python.org/3/library/os.path.html。

### 8.1.6 处理绝对路径和相对路径

• 调用 `os.path.abspath(path)`将返回参数的绝对路径的字符串。这是将相对路径转 换为绝对路径的简便方法。 

• 调用 `os.path.isabs(path)`，如果参数是一个绝对路径，就返回 True，如果参数是 一个相对路径，就返回 False。 

• 调用 `os.path.relpath(path, start)`将返回从 start 路径到 path 的相对路径的字符串。 如果没有提供 start，就使用当前工作目录作为开始路径。

```python
>>> os.path.abspath('.')
'C:\\Python34'
>>> os.path.abspath('.\\Scripts')
'C:\\Python34\\Scripts'
>>> os.path.isabs('.')
False
>>> os.path.isabs(os.path.abspath('.'))
True
```

```python
>>> os.path.relpath('C:\\Windows', 'C:\\')
'Windows'
>>> os.path.relpath('C:\\Windows', 'C:\\spam\\eggs')
'..\\..\\Windows'
>>> os.getcwd()
'C:\\Python34'
```

调用 `os.path.dirname(path)`将返回一个字符串，它包含 path 参数中最后一个斜杠之前的所有内容。

调用 `os.path.basename(path)`将返回一个字符串，它包含 path 参数中最后一个斜杠之后的所有内容。

```python
>>> path = 'C:\\Windows\\System32\\calc.exe'
>>> os.path.basename(path)
'calc.exe'
>>> os.path.dirname(path)
'C:\\Windows\\System32'
```

同时需要一个路径的目录名称和基本名称，就可以调用 `os.path.split()`，获 得这两个字符串的元组

```python
>>> calcFilePath = 'C:\\Windows\\System32\\calc.exe'
>>> os.path.split(calcFilePath)
('C:\\Windows\\System32', 'calc.exe')
```

调用 `os.path.dirname()`和 `os.path.basename()`，将它们的返回值放在 一个元组中，从而得到同样的元组。

```python
>>> (os.path.dirname(calcFilePath), os.path.basename(calcFilePath))
('C:\\Windows\\System32', 'calc.exe')
```

返回每个文件夹的字符串的列表, 使用 `split()`字符串方法, 并根据 `os.path.sep` 中的字符串进行分割

```python
>>> calcFilePath.split(os.path.sep)
['C:', 'Windows', 'System32', 'calc.exe']
```

### 8.1.7 查看文件大小和文件夹内容

• 调用 `os.path.getsize(path)`将返回 path 参数中文件的字节数。

• 调用 `os.listdir(path)`将返回文件名字符串的列表，包含 path 参数中的每个文件

```python
>>> os.path.getsize('C:\\Windows\\System32\\calc.exe')
776192
>>> os.listdir('C:\\Windows\\System32')
['0409', '12520437.cpx', '12520850.cpx', '5U877.ax', 'aaclient.dll',
--snip--
'xwtpdui.dll', 'xwtpw32.dll', 'zh-CN', 'zh-HK', 'zh-TW', 'zipfldr.dll']
```

如果想知道这个目录下所有文件的总字节数，就可以同时使用 `os.path.getsize()`和 `os.listdir()`。

```python
>>> totalSize = 0
>>> for filename in os.listdir('C:\\Windows\\System32'):
    totalSize = totalSize + os.path.getsize(os.path.join('C:\\Windows\\System32', filename))
>>> print(totalSize)
1117846456
```

### 8.1.8 检查路径有效性

• 如果 path 参数所指的文件或文件夹存在，调用 os.path.exists(path)将返回 True，否则返回 False。 

• 如果 path 参数存在，并且是一个文件，调用 os.path.isfile(path)将返回 True，否则返回 False。

 • 如果 path 参数存在，并且是一个文件夹，调用 os.path.isdir(path)将返回 True，否则返回 False。

```python
>>> os.path.exists('C:\\Windows')
True
>>> os.path.exists('C:\\some_made_up_folder')
False
>>> os.path.isdir('C:\\Windows\\System32')
True
>>> os.path.isfile('C:\\Windows\\System32')
False
>>> os.path.isdir('C:\\Windows\\System32\\calc.exe')
False
>>> os.path.isfile('C:\\Windows\\System32\\calc.exe')
True
```

利用 `os.path.exists()`函数，可以确定 DVD 或闪存盘当前是否连在计算机上。

```python
>>> os.path.exists('D:\\')
False
```

##  8.2 文件读写过程

在 Python 中，读写文件有 3 个步骤： 

1．调用 `open()`函数，返回一个 File 对象。 

2．调用 File 对象的 `read()`或 `write()`方法。 

3．调用 File 对象的 `close()`方法，关闭该文件。

### 8.2.1 用 open()函数打开文件 

`open()`函数返回一个 File 对象。

```python
>>> helloFile = open('C:\\Users\\your_home_folder\\hello.txt')
```

如果你不希望依赖于 Python 的默认值，也可以明确指明该模式，向 open()传入字符串'r'，作为第二个参数。所以open('/Users/asweigart/hello.txt', 'r')和 open('/Users/asweigart/hello.txt')做的事情一样。

### 8.2.2 读取文件内容

将整个文件的内容读取为一个字符串值，就使用 File 对象的 `read()`方法。

```python
>>> helloContent = helloFile.read()
>>> helloContent
'Hello world!'
```

使用 `readlines()`方法，从该文件取得一个字符串的列表。列表中的 每个字符串就是文本中的每一行。

```sonnet29.txt
When, in disgrace with fortune and men's eyes,
I all alone beweep my outcast state,
And trouble deaf heaven with my bootless cries,
And look upon myself and curse my fate,
```

```python
>>> sonnetFile = open('sonnet29.txt')
>>> sonnetFile.readlines()
[When, in disgrace with fortune and men's eyes,\n', ' I all alone beweep my
outcast state,\n', And trouble deaf heaven with my bootless cries,\n', And
look upon myself and curse my fate,']
```

### 8.2.3 写入文件

将`'w'`作为第二个参数传递给 `open()`，以写模式打开该文件。写模式覆写原有文件

将`'a'`作为第二个参数传递给 `open()`，以添加模式打开该文件。添加模式在末尾添加文本

在读取或写入文件后，调用 `close()`方法，然后才能再次打开该文件。

```python
>>> baconFile = open('bacon.txt', 'w')
>>> baconFile.write('Hello world!\n')
13
>>> baconFile.close()
>>> baconFile = open('bacon.txt', 'a')
>>> baconFile.write('Bacon is not a vegetable.')
25
>>> baconFile.close()
>>> baconFile = open('bacon.txt')
>>> content = baconFile.read()
>>> baconFile.close()
>>> print(content)
Hello world!
Bacon is not a vegetable.
```

`write()`方法不会像 `print()`函数那样，在字符串的末尾自动添加换行字符。必须自己添加该字符。

## 8.3 用 shelve 模块保存变量

```python
>>> import shelve
>>> shelfFile = shelve.open('mydata')
>>> cats = ['Zophie', 'Pooka', 'Simon']
>>> shelfFile['cats'] = cats
>>> shelfFile.close()
```

shelf 值不必用读模式或写模式打开，因为它们在打开后，既能读又能写。

```python
>>> shelfFile = shelve.open('mydata')
>>> type(shelfFile)
<class 'shelve.DbfilenameShelf'>
>>> shelfFile['cats']
['Zophie', 'Pooka', 'Simon']
>>> shelfFile.close()
```

 这些方法返回类似列表的值，而不是真正的列表，所以应该将它们传递给 list()函数，取得列表的形式。

```python
>>> shelfFile = shelve.open('mydata')
>>> list(shelfFile.keys())
['cats']
>>> list(shelfFile.values())
[['Zophie', 'Pooka', 'Simon']]
>>> shelfFile.close()
```

## 8.4 用 pprint.pformat()函数保存变量

pprint.pformat()函数将将列表或字典中的内容返回为字符串类型

```python
>>> import pprint
>>> cats = [{'name': 'Zophie', 'desc': 'chubby'}, {'name': 'Pooka', 'desc': 'fluffy'}]
>>> pprint.pformat(cats)
"[{'desc': 'chubby', 'name': 'Zophie'}, {'desc': 'fluffy', 'name': 'Pooka'}]"
>>> fileObj = open('myCats.py', 'w')
>>> fileObj.write('cats = ' + pprint.pformat(cats) + '\n')
83
>>> fileObj.close()
```

```python
>>> import myCats
>>> myCats.cats
[{'name': 'Zophie', 'desc': 'chubby'}, {'name': 'Pooka', 'desc': 'fluffy'}]
>>> myCats.cats[0]
{'name': 'Zophie', 'desc': 'chubby'}
>>> myCats.cats[0]['name']
'Zophie'
```







