---
layout:     post   				    # 使用的布局（不需要改）
title:      从Excel到Python笔记 	 # 标题 
subtitle:   数据分析入门             #副标题
date:       2018-12-12 				# 时间
author:     LY 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - 数据分析
---

## 
>
import numpy as np
import pandas as pd
下面分别是从Excel和csv格式文件中导入数据并创建数据表的方法
df=pd.DataFrame(pd.read_csv('name.csv',header=1))
df=pd.DataFrame(pd.read_Excel('name.xlsx'))





















