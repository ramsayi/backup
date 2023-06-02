---
title: 《Python编程快速上手》7.15 项目：电话号码和 E-mail 地址提取程序
tags:
  - Python
categories:
  - 技术学习
  - Python
  - Python编程快速上手
abbrlink: 88d93796
cover: /assets/img/post/Python.webp
date: 2022-01-21 15:12:50
---

###### phoneAndEmail.py - 电话号码和 E-mail 地址提取程序

```python
#! python3
# phoneAndEmail.py - 电话号码和 E-mail 地址提取程序

import pyperclip, re

phoneRegex = re.compile(r'''(
    (\d{3}|\(\d{3}\))?                  # area code
    (\s|-|\.)?                          # separator
    (\d{3})                             # first 3 digits
    (\s|-|\.)                           # separator
    (\d{4})                             # last 4 digits
    (\s*(ext|x|ext.)\s*(\d{2,5}))?      # extension
    )''', re.VERBOSE)

# Create email regex.
emailRegex = re.compile(r'''(
    [a-zA-Z0-9._%+-]+       # username
    @                       # @ symbol
    [a-zA-Z0-9.-]+          # domain name
    (\.[a-zA-Z]{2,4})       # dot-something
    )''', re.VERBOSE)

# Find matches in clipboard text.
text = str(pyperclip.paste())
matches = []
for groups in phoneRegex.findall(text):
    phoneNum = '-'.join([groups[1], groups[3], groups[5]])
    if groups[8] != '':
        phoneNum += ' x' + groups[8]
    matches.append(phoneNum)
for groups in emailRegex.findall(text):
    matches.append(groups[0])

print(matches)

# Copy results to the clipboard.
if len(matches) > 0:
    pyperclip.copy('\n'.join(matches))
    print('Copied to clipboard:')
    print('\n'.join(matches))
else:
    print('No phone numbers or email addresses found.')
```

###### 示例文本

```text
Contact Us

No Starch Press, Inc.
245 8th Street
San Francisco, CA 94103 USA
Phone: 800.420.7240 or +1 415.863.9900 (9 a.m. to 5 p.m., M-F, PST)
Fax: +1 415.863.9950

Reach Us by Email

General inquiries: info@nostarch.com
Media requests: media@nostarch.com
Academic requests: academic@nostarch.com (Further information)
Conference and Events: conferences@nostarch.com
Help with your order: info@nostarch.com
Reach Us on Social Media
Twitter
Facebook
Instagram
Linkedin
Pinterest
```

###### 输出

```shell
['800-420-7240', '415-863-9900', '415-863-9950', 'info@nostarch.com', 'media@nostarch.com', 'academic@nostarch.com', 'conferences@nostarch.com', 'info@nostarch.com']
Copied to clipboard:
800-420-7240
415-863-9900
415-863-9950
info@nostarch.com
media@nostarch.com
academic@nostarch.com
conferences@nostarch.com
info@nostarch.com
```

