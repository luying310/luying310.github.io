---
layout:     post
title:      Excel
subtitle:   Excel数据分析常用函数
date:       2018-11-12
author:     LY
header-img: img/post-bg-kuaidi.jpg
catalog: true
tags:	
    - Excel
    

---

# Excel 2016

Excel函数比较简单，可以根据函数参数和帮助实现简单的函数处理。复杂的嵌套多层函数写起来比较麻烦，可以寻找其他方式替代。

## 1. 文本清洗函数
### Find
	
	=FIND(Find_text, Within_text, Start_num)
	=FIND(找什么, 在哪儿找, [从第几个开始, 1])返回的是数字。

### Left

	=LEFT(text, Start_num)
	=LEFT(文本, [要几个，1])返回的是字符串。

### Right

	=RIGHT(text, Start_num)
	=RIGHT(文本, [要几个，1])返回的是字符串。

### Mid
	
	=MID(text, Start_num, num_chars)
	=MID(文本, 哪开始，[要几个，1])返回的是字符串。

### Concatenate

	=CONCATENATE(text1, [text2], ...)
	=CONCATENATE(合并文本1，[合并文本2]……])返回的是字符串。

### Replace

	=REPLACE(old_text, start_num, num_chars, new_text)
	=REPLACE(老字符串，从哪开始，去掉几个，新字符串)返回的是字符串。

### Substitute

	=SUBSTITUTE(text, old_text, new_text, [instance_num])
	=SUBSTITUTE(需要换的字符串，老字符串，新字符串，[第几个老字符串])返回的是字符串。

### replace和substitute的区别

replace要指定第几个到第几个字符（数字），substitute则是找到包含的老字符，替换成新字符。

### Text

	=TEXT(value, format_text)
	=TEXT(值，格式)返回的是指定格式的文本。

### Trim

	=TRIM(text)
	=TRIM(值)返回的是头尾去掉空格的文本。

### Len

	=LEN(text)
	=LEN(字符串)返回的是长度

## 2.关联匹配函数

### Lookup
	
	=LOOKUP(lookup_value, lookup_vector, result_vector)
	=LOOKUP(要查找的值，查找值得表，返回值得表)返回的是返回表中对应的那个值。

### Vlookup

	=VLOOKUP（要查找的值、要在其中查找值的区域、区域中包含返回值的列号、精确匹配或近似匹配 – 指定为 0/FALSE 或 1/TRUE）

### Index

数组形式：INDEX(array，row_num，column_num)返回某个区域中指定行列的值。

引用形式：INDEX(reference，row_num，column_num，[area_num, 1])返回某个或多个区域中指定行列的值。

（数组形式通常返回数值或数值数组；引用形式通常返回引用。）

### Match

返回指定值在数列中的序号。

MATCH（lookup_value,lookuparray,match-type）

lookup_value：表示查询的指定内容；

lookuparray：表示查询的指定区域；

match-type：表示查询的指定方式，用数字-1、0或者1表示。

1：小于或等于的最大值，必须升序

0：等于

-1：大于或等于的最小值，必须降序

### Row

返回行数

### Column

返回列数

### Offset

偏移

### Hyperlink

超链接

## 3.计算统计函数

### Sum

求和

### Sumif

条件求和

### Sumproduct

两列，可以相乘后累加。

### count

计数

### countif

条件计数。

### Rank

查找某个数字的排名

### Rand Randbetween

随机生成某个范围内的数字

### Average

平均数

### Quartile

分位数

### Stdev

标准差

### Substotal

函数中的函数？？

### Int

数字取整

### Round

四舍五入

### ABS

绝对值
 
## 4.时间序列函数

Year

Month

Weekday

Weeknum

Day

Date

Now

Today

## 5.逻辑运算函数

false=0，true=1.

And

Or

If

Is（iserror、isnum）

Not
