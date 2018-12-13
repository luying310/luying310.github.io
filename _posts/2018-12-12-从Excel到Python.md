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
	
	- pandas 
	
	- numpy
---

# 通过Python完成数据生成和导入、清洗、分类、筛选、分类汇总、透视等最常见的操作。
## 1.导入数据表   
import numpy as np
  
import pandas as pd
  
df=pd.DataFrame(pd.read_csv('name.csv',header=1))
  
df=pd.DataFrame(pd.read_Excel('name.xlsx'))
  
## 2.创建数据表
df = pd.DataFrame({"id":[1001,1002,1003,1004,1005,1006],  
"date":pd.date_range('20130102', periods=6),
"city":['Beijing ', 'SH', ' guangzhou ', 'Shenzhen', 'shanghai', 'BEIJING '],
"age":[23,44,54,32,34,32],
"category":['100-A','100-B','110-A','110-C','210-A','130-F'],
"price":[1200,np.nan,2133,5433,np.nan,4432]},
  
columns =['id','date','city','category','age','price'])
  
df.shape#查看数据表的维度行列

(6, 6)#返回结果

df.info()#数据表信息

df.dtypes#查看数据表各列格式

df.isnull()#检查数据空值

df['price'].isnull()#检查特定列空值

df['city'].unique()#查看city列中的唯一值

df.values#查看数据表的值

df.columns#查看列名称

df.head(3)#查看前3行数据

df.tail(3)#查看最后3行

df.dropna(how='any')#删除数据表中含有空值的行

df.fillna(value=0)#使用数字0填充数据表中空值

df['price'].fillna(df['price'].mean())#使用price均值对NA进行填充

df['city']=df['city'].map(str.strip)#清除city字段中的字符空格

df['city']=df['city'].str.lower()#city列大小写转换

df['price'].astype('int')#更改数据格式

df.rename(columns={'category': 'category-size'})#更改列名称

df['city'].drop_duplicates()#删除后出现的重复值

df['city'].drop_duplicates(keep='last')#删除先出现的重复值

df['city'].replace('sh', 'shanghai')#数据替换

df1=pd.DataFrame({"id":[1001,1002,1003,1004,1005,1006,1007,1008],
"gender":['male','female','male','female','male
','female','male','female'],
"pay":['Y','N','Y','Y','N','Y','N','Y',],
"m-point":[10,12,20,40,40,40,30,20]})

df_inner=pd.merge(df,df1,how='inner')#Inner数据表匹配合并

df_left=pd.merge(df,df1,how='left')#left数据表匹配合并

df_right=pd.merge(df,df1,how='right')#right数据表匹配合并

df_outer=pd.merge(df,df1,how='outer')#outer数据表匹配合并

df_inner.set_index('id')#设置索引列

df_inner.sort_values(by=['age'])#按特定列的值排序

df_inner.sort_index()#按索引列排序

df_inner['group'] = np.where(df_inner['price'] > 3000,'high','low')#如果price列的值>3000，group列显示high，否则显示low

df_inner.loc[(df_inner['city'] == 'beijing') & (df_inner['price']>= 4000), 'sign']=1#对复合多个条件的数据进行分组标记

pd.DataFrame((x.split('-') for x in df_inner['category']),index=df_inner.index,columns=['category','size'])#对category字段的值依次进行分列，并创建数据表，索引值为df_inner的索引列，列
名称为category和size

df_inner=pd.merge(df_inner,split,right_index=True, left_index=True)#将完成分列后的数据表与原df_inner数据表进行匹配

df_inner.loc[3]#按索引提取单行的数值

df_inner.loc[0:5]#按索引提取区域行数值

df_inner.reset_index()#重设索引

df_inner=df_inner.set_index('date')#设置日期为索引

df_inner[:'2013-01-04']#提取4日之前的所有数据

df_inner.iloc[:3,:2]#使用iloc按位置区域提取数据

df_inner.iloc[[0,2,5],[4,5]]#使用iloc按位置单独提取数据

df_inner.ix[:'2013-01-03',:4]#使用ix按索引标签和位置混合提取数据

df_inner['city'].isin(['beijing'])#判断city列的值是否为beijing

df_inner.loc[df_inner['city'].isin(['beijing','shanghai'])]#先判断city列里是否包含beijing和shanghai，然后将复合条件的数据提取出来。

pd.DataFrame(category.str[:3])#提取前三个字符，并生成数据表

df_inner.loc[(df_inner['age'] > 25) & (df_inner['city'] == 'beijing'), ['id','city','age','category','gender']]/#使用“与”条件进行筛选

df_inner.loc[(df_inner['age'] > 25) | (df_inner['city'] == 'beijing'), ['id','city','age','category','gender']].sort(['age'])#使用“或”条件筛选

df_inner.loc[(df_inner['age'] > 25) | (df_inner['city'] == 'beijing'), ['id','city','age','category','gender','price']].sort(['age']).price.sum()
#对筛选后的数据按price字段进行求和

df_inner.loc[(df_inner['city'] != 'beijing'), ['id','city','age','category','gender']].sort(['id'])#使用“非”条件进行筛选

df_inner.loc[(df_inner['city'] != 'beijing'), ['id','city','age','category','gender']].sort(['id']).city.count()#对筛选后的数据按city列进行计数

df_inner.query('city == ["beijing", "shanghai"]')#使用query函数进行筛选

df_inner.query('city == ["beijing", "shanghai"]').price.sum()#对筛选后的结果按price进行求和

df_inner.groupby('city').count()/#对所有列进行计数汇总

df_inner.groupby('city')['id'].count()#对特定的ID列进行计数汇总

df_inner.groupby(['city','size'])['id'].count()#对两个字段进行汇总计数

df_inner.groupby('city')['price'].agg([len,np.sum, np.mean])#对city字段进行汇总并计算price的合计和均值。

pd.pivot_table(df_inner,index=["city"],values=["price"],columns=["size"],aggfunc=[len,np.sum],fill_value=0,margins=True)#数据透视表

df_inner.sample(n=3)#简单的数据采样

weights = [0, 0, 0, 0, 0.5, 0.5]#手动设置采样权重

df_inner.sample(n=2, weights=weights)#手动设置采样权重

df_inner.sample(n=6, replace=False)#采样后不放回

df_inner.sample(n=6, replace=True)#采样后放回

df_inner.describe().round(2).T#数据表描述性统计

df_inner['price'].std()#标准差

df_inner['price'].cov(df_inner['m-point'])#两个字段间的协方差

df_inner.cov()#数据表中所有字段间的协方差

df_inner['price'].corr(df_inner['m-point'])#相关性分析

df_inner.corr()#数据表相关性分析

df_inner.to_Excel('Excel_to_Python.xlsx', sheet_name='bluewhale_cc')#输出到Excel格式

df_inner.to_csv('Excel_to_Python.csv')#输出到CSV格式





