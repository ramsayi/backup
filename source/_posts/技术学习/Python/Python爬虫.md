---
title: Python从零开始学编程爬虫
tags:
  - Python
  - 爬虫
categories:
  - 技术学习
  - Python
cover: '/assets/img/post/Python-Spider.webp'
abbrlink: c386cf1b
date: 2022-07-09 10:13:20
---

# requests 模块基础

## 01.requests第一血.py

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
# 需求：爬取搜狗首页的页面数据
import requests

if __name__ == "__main__":
    # 1.指定url
    url = 'https://www.sogou.com/'
    # 2.发起请求
    response = requests.get(url=url)
    # 3.获取相应数据
    page_text = response.text
    print(page_text)
    # 4.持久化存储
    with open('./sogou.html', 'w', encoding='utf-8') as fp:
        fp.write(page_text)
    print('爬取数据结束!')
    
```

## 02.requests实战之网页采集器.py

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import requests

if __name__ == "__main__":
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36'
    }
    url = 'https://www.sogou.com/web'
    kw = input('输入关键词：')
    param = {
        'query': kw
    }
    response = requests.get(url=url, params=param, headers=headers)
    page_text = response.text
    filename = kw + '.html'
    with open(filename, 'w', encoding='utf-8') as fp:
        fp.write(page_text)
    print(filename, '保存成功！')
    
```

## 03.requests实战之破解百度翻译.py

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import requests
import json

if __name__ == "__main__":
    post_url = 'https://fanyi.baidu.com/sug'
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36'
    }
    word = input('输入单词：')
    data = {
        'kw': word
    }
    response = requests.post(url=post_url, data=data, headers=headers)
    # json()方法返回的是对象
    dic_obj = response.json()
    fileName = word + '.json'
    fp = open(fileName, 'w', encoding='utf-8')
    json.dump(dic_obj, fp=fp, ensure_ascii=False)
    print('爬取结束！')
    
```

## 04.requests实战之豆瓣电影爬取.py

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import requests
import json

if __name__ == "__main__":
    url = 'https://movie.douban.com/j/chart/top_list'
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36'
    }
    param = {
        'type': '24',
        'interval_id': '100:90',
        'action': '',
        'start': '0',  # 从第几部开始取
        'limit': '20'  # 取的个数
    }
    response = requests.get(url=url, params=param, headers=headers)
    list_data = response.json()
    fp = open('./douban.json', 'w', encoding='utf-8')
    json.dump(list_data, fp=fp, ensure_ascii=False)
    print('爬取结束！')

```

# 数据解析

## 0.爬取图片.py

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import re

import requests

if __name__ == "__main__":
    url = 'https://product.360che.com/img/c1_s66_b5_s6879_m118627_t31.html'
    img_data = requests.get(url=url).content
    with open('./pic.jpg', 'wb') as fp:
        fp.write(img_data)

```

## 1.正则解析.py

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import requests
import re
import os

if __name__ == "__main__":
    # 创建一个文件夹，保存所有图片
    if not os.path.exists('./trucks'):
        os.mkdir('./trucks')

    url = 'https://product.360che.com/img/c1_s66_b5_s6879_m118627_t31.html'
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36'
    }
    # 使用通用爬虫对url对应的一整张页面进行爬取
    page_text = requests.get(url=url, headers=headers).text

    # 使用聚焦爬虫将页面中所有的图片进行解析/提取
    ex = '<dt><a.*?<img src="(.*?)" border.*?width="240".*?></a></dt>'
    img_src_list = re.findall(ex, page_text, re.S)
    print(img_src_list)

    for src in img_src_list:
        # 请求到了图片二进制数据
        img_data = requests.get(url=src, headers=headers).content
        # 拆分图片名称
        img_name = src.split('/')[-1]
        # 路径拼接
        imgPath = './trucks/' + img_name
        with open(imgPath, 'wb') as fp:
            fp.write(img_data)
            print(img_name, '下载成功！')

```

## 2.正则解析-分页爬取.py

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import requests
import re
import os

if __name__ == "__main__":
    # 创建一个文件夹，保存所有图片
    if not os.path.exists('./trucks'):
        os.mkdir('./trucks')

    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36'
    }
    # 设置一个通用的url模板
    url = 'https://product.360che.com/img/c1_s66_b5_s6879_m118627_t32_c%d.html'
    for pageNum in range(1, 3):
        new_url = format(url % pageNum)

        # 使用通用爬虫对url对应的一整张页面进行爬取
        page_text = requests.get(url=new_url, headers=headers).text

        # 使用聚焦爬虫将页面中所有的图片进行解析/提取
        ex = '<dt><a.*?<img src="(.*?)" border.*?width="240".*?></a></dt>'
        img_src_list = re.findall(ex, page_text, re.S)
        print(img_src_list)

        for src in img_src_list:
            # 请求到了图片二进制数据
            img_data = requests.get(url=src, headers=headers).content
            # 拆分图片名称
            img_name = src.split('/')[-1]
            # 路径拼接
            imgPath = './trucks/' + img_name
            with open(imgPath, 'wb') as fp:
                fp.write(img_data)
                print(img_name, '下载成功！')

```

## 3.bs4解析基础.py

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
from bs4 import BeautifulSoup

if __name__ == "__main__":
    # 将本地的html文件加载到该对象中
    fp = open('./test.html', 'r', encoding='utf-8')
    soup = BeautifulSoup(fp, 'lxml')
    print(soup.select('ul > li a')[1]['href'])

    # soup.tagName

    # soup.find('tagName')
    # soup.find('tagName', class_/id/attr='XXX')
    # soup.find_all('tagName')

    # select('某种选择器')，返回一个列表
    # soup.select('.tang > ul > li > a')，'>'表示层级选择
    # soup.select('.tang > ul a'), '空格'表示多个层级

    # 获取标签之间的文本数据
    # soup.a.text/string/get_text()
    # text/get_text()获取所有文本内容  string只可以获取直系文本内容

    # 获取标签中属性值
    # soup.a['href']

```

## 4.bs4案例.py

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import requests
from bs4 import BeautifulSoup

if __name__ == "__main__":
    # 爬取首页数据
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36'
    }
    url = "https://www.shicimingju.com/book/sanguoyanyi.html"
    page_text = requests.get(url=url, headers=headers).content.decode('utf-8')

    # 解析出标题和详情url
    soup = BeautifulSoup(page_text, 'lxml')
    a_list = soup.select('.book-mulu > ul > li a')
    fp = open('./sanguo.txt', 'w', encoding='utf-8')
    for a in a_list:
        title = a.string
        detail_url = 'https://www.shicimingju.com/' + a['href']
        # print(title, detail_url)
        # 对详情页发起请求，解析出章节内容
        detail_page_text = requests.get(url=detail_url, headers=headers).content.decode('utf-8')
        detail_soup = BeautifulSoup(detail_page_text, 'lxml')
        div_tag = detail_soup.find('div', class_='chapter_content')
        content = div_tag.text
        fp.write(title + ':' + content + '\n')
        print(title + '爬取成功！')

```







