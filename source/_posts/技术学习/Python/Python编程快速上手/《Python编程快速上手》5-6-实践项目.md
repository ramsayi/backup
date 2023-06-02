---
title: 《Python编程快速上手》5.6 实践项目
tags:
  - Python
categories:
  - 技术学习
  - Python
  - Python编程快速上手
abbrlink: 6d427ba9
cover: /assets/img/post/Python.webp
date: 2022-01-22 22:12:26
---

### 5.6.1 好玩游戏的物品清单

```python
stuff = {'rope': 1, 'torch': 6, 'gold coin': 42, 'dagger': 1, 'arrow': 12}

def displayInventory(inventory):
    print('Inventory:')
    item_total = 0
    for k, v in inventory.items():
        print(str(v) + ' ' + k)
        item_total += v
    print("Total number of items: " + str(item_total))

displayInventory(stuff)
```

###### 输出

```text
Inventory:
1 rope
6 torch
42 gold coin
1 dagger
12 arrow
Total number of items: 62
```

### 5.6.2 列表到字典的函数，针对好玩游戏物品清单

```python
def addToInventory(inventory, addedItems):
    for i in addedItems:
        if i in inventory:
            inventory[i] += 1
        else:
            inventory[i] = 1
    return inventory

def displayInventory(inventory):
    print('Inventory:')
    item_total = 0
    for k, v in inventory.items():
        print(str(v) + ' ' + k)
        item_total += v
    print("Total number of items: " + str(item_total))

inv = {'gold coin': 42, 'rope': 1}
dragonLoot = ['gold coin', 'dagger', 'gold coin', 'gold coin', 'ruby']
inv = addToInventory(inv, dragonLoot)
displayInventory(inv)
```

###### 输出

```text
Inventory:
45 gold coin
1 rope
1 dagger
1 ruby
Total number of items: 48
```

