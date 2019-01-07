---
layout:     post
title:      Mysql
subtitle:   mysql学习
date:       2018-11-12
author:     LY
header-img: img/post-bg-kuaidi.jpg
catalog: true
tags:
    - MySQL	
    - Excel
    

---

# MySQL
## 1.安装mysql和navicat
## 2.生成数据表
### 2.1 导入数据表
用代码导入数据比较麻烦，尤其是很多数据的列比较多，所以一般用navicat等图形工具导入比较方便。注：导入数据时注意修改属性，可以设置成有错误时停止，方便修改。
### 2.2 创建数据表
    #创建数据表字段
    CREATE TABLE data1(id INT(10), Record_date DATE, city VARCHAR(255),age VARCHAR(255), category VARCHAR(255), price FLOAT(10));
    SELECT * FROM data1;
    #创建数据表data2
    CREATE TABLE data2(id INT(10),gender VARCHAR(255),pay VARCHAR(255), mp VARCHAR(255));
    SELECT * FROM data2;
	#插入值
    INSERT INTO
    data2(id, gender,pay, mp)
    VALUES
    (1001, 'male', 'Y',10),
	(1002, 'female', 'N', 12),
	(1003, 'male', 'Y', 20),
	(1004, 'female', 'Y', 40),
	(1005, 'male', 'N', 40),
	(1006, 'female', 'Y', 40),
	(1007, 'male', 'N', 30),
	(1008, 'female', 'Y', 20);
	SELECT * FROM data2;

## 3.数据表检查

### 3.1 数据维度(行列)

    #查看数据条数
    SELECT COUNT(*) FROM data1;
    #查看数据表2的字段数量
    SELECT COUNT(*) as column_num FROM information_schema.`COLUMNS` WHERE TABLE_NAME='data2';

### 3.2 数据表信息

	#查看数据表信息
	DESC data1;

### 3.3 查看空值

	#查看price为空的数据
	SELECT * FROM data1 WHERE price IS NULL;
	#查看price为0的数据
	SELECT * FROM data1 WHERE price=0;

### 3.4 查看唯一值

	#查询单列唯一值
	SELECT DISTINCT (city)FROM data1;

### 3.5 查看列名称

	#查看数据表列名称
	SHOW COLUMNS FROM data1;

### 3.6 查看前3行数据

	#查看数据表前3行
	SELECT * FROM data1 LIMIT 3;

## 4. 数据表清洗

### 4.1 处理缺失值(填充)

	#计算price列的均值
	SELECT ROUND(AVG(price),2) AS avg_price FROM data1;
	#使用均值填充0值
	UPDATE data1 SET price=2199.67 WHERE price=0;

### 4.2 清理空格

	#清理字符中的空格
	UPDATE data1 SET city=TRIM(city);
	select city from data1;

### 4.3 数值修改及替换

	#修改和替换
	UPDATE data1 SET city=REPLACE(city,'SH','shanghai');
	SELECT city FROM data1;

### 4.4 大小写转换

	#大小写转换
	UPDATE data1 SET city=LOWER/UPPER(city);
	select city from data1;

## 5. 数据预处理

### 5.1 数据表匹配合并

	#INNER JOIN匹配查询
	SELECT record_date, city, age, category, price,gender,pay,mp FROM
	data1 INNER JOIN data2 ON data1.id=data2.id;
	# LEFT JOIN匹配查询
	SELECT record_date, city, age, category, price,gender,pay,mp FROM
	data1 LEFT OUTER JOIN data2 ON data1.id=data2.id;
	# RIGHT JOIN匹配查询
	SELECT record_date, city, age, category, price,gender,pay,mp FROM
	data1 RIGHT OUTER JOIN data2 ON data1.id=data2.id;

### 5.2 数据排序

	#数据升序排序
	SELECT * FROM data1 ORDER BY age;
	#数据降序排序
	SELECT * FROM data1 ORDER BY age DESC;
	#多多列数据进行排序
	SELECT * FROM data1 ORDER BY age,price DESC;

### 5.3 数据分组

	#age字段分组
	SELECT age,
	CASE
	WHEN age<30 THEN 'A'
	WHEN age>=30 AND age<50 THEN 'B'
	WHEN age>=50 THEN 'C'
	ELSE 'D' END AS age_type
	FROM data1;
	#直接分组查询并汇总
	SELECT COUNT(id) AS id_count, SUM(price)AS total_price,
	CASE
	WHEN age<30 THEN 'A'
	WHEN age>=30 AND age<50 THEN 'B'
	WHEN age>=50 THEN 'C'
	ELSE 'D' END AS age_type
	FROM data1 GROUP BY age_type ORDER BY id_count;

### 5.4 数据分列

	#数据分列
	SELECT SUBSTRING_INDEX(category,'-',1)AS size,SUBSTRING_INDEX(category,'-',-1)AS colour FROM data1;
	SELECT id,Record_date,city,age,category,price,SUBSTRING_INDEX(category,'-',1)AS size,SUBSTRING_INDEX(category,'-',-1)AS colour FROM data1;
	#按分列后的结果进行单列数据汇总
	SELECT SUBSTRING_INDEX(category,'-',1) AS size,COUNT(id) FROM data1 GROUP BY size;
	#按分列后的结果进行多列数据汇总
	SELECT SUBSTRING_INDEX(category,'-',1) AS size,COUNT(id) AS id_count,ROUND(SUM(price),2) AS total_price FROM data1 GROUP BY size;
	#数据分列（改表）
	#添加两个空字段
	ALTER TABLE data1 ADD (size VARCHAR(255),colour VARCHAR(255));
	SELECT * FROM data1;
	#更新分列后的字段内容
	UPDATE data1 SET size = SUBSTRING_INDEX(category,'-',1),colour =SUBSTRING_INDEX(category,'-',-1);
	SELECT * FROM data1;

## 6. 数据提取

### 6.1 按列提取数据

	#按列提取
	SELECT city FROM data1;

### 6.2 按行提取数据

	#按行提取
	SELECT * FROM data1 WHERE city='beijing';

### 6.3 按位置提取数据

	#按位置提取
	SELECT * FROM data1 LIMIT 2,5;

### 6.4 按条件提取数据

	#按条件提取并计算
	SELECT AVG(price) FROM data1 WHERE city='beijing' AND age<25;

## 7. 数据筛选

	#数据筛选AND
	SELECT * FROM data1 WHERE city='shanghai' AND age>30;
	#数据筛选IN
	SELECT * FROM data1 WHERE city IN ('shanghai','beijing');
	#数据筛选OR
	SELECT * FROM data1 WHERE city='shanghai' OR age>30;
	#数据筛选(不等于)
	SELECT * FROM data1 WHERE city !='beijing';
	#数据筛选like(模糊筛选)
	SELECT * FROM data1 WHERE city LIKE 'bei%';
	#筛选后计数 countif
	SELECT COUNT(id) AS id_count FROM data1 WHERE city='shanghai'AND age>30;
	#筛选后求和 sumtif
	SELECT SUM(price) AS price FROM data1 WHERE city='beijing' AND age<30;
	#筛选后求均值 averageif
	SELECT AVG(price) AS avg_price FROM data1 WHERE city !='beijing';

## 8. 数据分类汇总及透视

### 8.1 分类汇总

	#单列分类汇总
	SELECT city,COUNT(id) AS id_count FROM data1 GROUP BY city ORDER BY id_count;
	#多列分类汇总
	SELECT city,colour,ROUND(SUM(price),2) AS id_count FROM data1 GROUP BY city,colour;

### 8.2 数据透视

	#查看原始数据表
	SELECT * FROM data1;
	#使用CASE WHEN进行数据透视
	CREATE VIEW data_Items AS (
	SELECT
	data1.city,
	CASE WHEN colour = "A" THEN price END AS A,
	CASE WHEN colour = "B" THEN price END AS B,
	CASE WHEN colour = "C" THEN price END AS C,
	CASE WHEN colour = "F" THEN price END AS F
	FROM data1
	);
	#查看结果
	SELECT * FROM data_Items;
	#对字段进行求和汇总
	CREATE VIEW data1_Extended_Pivot AS (
	SELECT
	city,
	SUM(A) AS A,
	SUM(B) AS B,
	SUM(C) AS C,
	SUM(F) AS F
	FROM data_Items
	GROUP BY city
	);
	#查看结果
	SELECT * FROM data1_Extended_Pivot;
	#对空值进行处理
	CREATE VIEW data1_Extended_Pivot_Pretty AS (
	SELECT
	city,
	COALESCE(A, 0) AS A,
	COALESCE(B, 0) AS B,
	COALESCE(C, 0) AS C,
	COALESCE(F, 0) AS F
	FROM data1_Extended_Pivot
	);
	#查看数据透视结果
	SELECT * FROM data1_Extended_Pivot_Pretty;
