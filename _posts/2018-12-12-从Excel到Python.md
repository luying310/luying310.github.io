---
layout:     post
title:      从excel到python笔记
subtitle:   用python实现Excel的部分功能
date:       2018-12-12
author:     LY
header-img: img/post-bg-kuaidi.jpg
catalog: true
tags:
    - python
    - Excel
---

# 通过Python完成数据生成和导入、清洗、分类、筛选、分类汇总、透视等最常见的操作。
## 1.导入数据表   
import numpy as np-
import pandas as pd-
df=pd.DataFrame(pd.read_csv('name.csv',header=1))-
df=pd.DataFrame(pd.read_Excel('name.xlsx'))-
## 2.创建数据表
df = pd.DataFrame({"id":[1001,1002,1003,1004,1005,1006],
"date":pd.date_range('20130102', periods=6),
"city":['Beijing ', 'SH', ' guangzhou ', 'Shenzhen', 'shanghai', 'BEIJING '],
"age":[23,44,54,32,34,32],
"category":['100-A','100-B','110-A','110-C','210-A','130-F'],
"price":[1200,np.nan,2133,5433,np.nan,4432]},-
columns =['id','date','city','category','age','price'])-
img/num1-1.jpg