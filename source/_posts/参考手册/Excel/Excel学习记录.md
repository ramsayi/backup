---
title: Excel学习记录
tags:
  - Excel
categories:
  - 参考手册
  - Excel
abbrlink: f2029d3b
date: 2021-11-15 22:36:00
---

# Excel基本操作

## [函数名称自动补全](https://jingyan.baidu.com/article/20b68a8854a719796cec62bb.html)

按`Tab`输入，按`↓` `↑`对列出的函数进行选择

## [制作独立式图表](https://jingyan.baidu.com/article/ce09321b28954b6afe858f2f.html)

Ctrl + 1 设置单元格格式

# 函数

## 求和

一般的求和函数

```excel
=SUM(C3:E3)
```

## 排序

区域`F3:F13`必须用绝对引用，因为要拖动，而区域不能改变

`0`按降序排序，`1`按升序排序

```excel
=RANK(F3,$F$3:$F$13,0)
```

## 条件与和或

条件AND(与)必须3个条件同时满足，则条件为真(true)，公式值为优；否则，为假(false)，值为良

```excel
=IF(AND(C3>80,D3>80,E3>80),"优","良")
```

条件OR(或)只须3个条件有1个满足，则条件为真(true)，公式值为优；否则(即3个条件都不满足)，
为假(false)，值为及格

```excel
=IF(OR(C3>95,D3>95,E3>95),"优","及格")
```

## [统计最高分和最低分](https://jingyan.baidu.com/article/6fb756ecf70cbc641958fb14.html)

```excel
=MAX(A1:A9)
```

```excel
=MIN(A1:A9)
```

## [统计非白单元格的数量](https://support.microsoft.com/zh-cn/office/counta-%E5%87%BD%E6%95%B0-7dc98875-d5c1-46f1-9a82-53f3219e2509)

```excel
=COUNTA (A2:A6)
```

## 统计不重复数据个数

```excel
=SUMPRODUCT(1/COUNTIF(A1:A8,A1:A8))
```

## [将每行数据前3名设置为红色填充](https://www.zhihu.com/zvideo/1434122654815399936)

```excel
=$G3>=LARGE($G$3:$G$12,3)
```

## [TRANSPOSE 函数](https://support.microsoft.com/zh-cn/office/transpose-%E5%87%BD%E6%95%B0-ed039415-ed8a-4a81-93e9-4b6dfac76027)

## [WEEKDAY 函数](https://support.microsoft.com/zh-cn/office/weekday-%E5%87%BD%E6%95%B0-60e44483-2ed1-439f-8bd0-e404c190949a)

## [Excel ROW 函数](https://www.lanrenexcel.com/excel-row-function/)

## [Excel ISODD 函数](https://www.lanrenexcel.com/excel-isodd-function/)



# 外部链接

## [Excel 中的键盘快捷方式](https://support.microsoft.com/zh-cn/office/excel-%E4%B8%AD%E7%9A%84%E9%94%AE%E7%9B%98%E5%BF%AB%E6%8D%B7%E6%96%B9%E5%BC%8F-1798d9d5-842a-42b8-9c99-9b7213f0040f)

## [Excel 快捷键大全（GIF） - 懒人Excel](https://jingyan.baidu.com/article/20b68a8854a719796cec62bb.html)





