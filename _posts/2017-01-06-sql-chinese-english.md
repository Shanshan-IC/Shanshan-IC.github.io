---
layout:     post
title:      "SQL Chinese in string"
category:   SQL 
tags:       SQL
---
* content
{:toc}

It works  in MySQL!
```sql
show databases;

USE mysql;

CREATE TABLE test (
	id INT(11),
	name VARCHAR(25)
);

INSERT INTO test VALUES(1, "23");
INSERT INTO test VALUES(1, "测试");
INSERT INTO test VALUES(1, "12测试");

-- start with Chinese
SELECT name FROM test WHERE ascii(name) > 127;
-- start with no Chinese
SELECT name FROM test WHERE ascii(name) < 127;

-- Chinese
select * from test where name like '%[吖-座]%';
-- number


-- ascii code
-- number: 48 - 57, letter: 65 - 123, chinese: 123+
-- delete all the numbers values
SELECT * FROM test WHERE ascii(name) between 48 and 57;

-- 
SELECT name, 
	CASE name REGEXP "[u0391-uFFE5]"
		WHEN 1 THEN "不是中文字符"
		ELSE "是中文字符"
	END AS "判断是否是中文字符"
FROM test;

-- length:是计算字段的长度一个汉字是算三个字符,一个数字或字母算一个字符
-- char_length:不管汉字还是数字或者是字母都算是一个字符
-- 检查是否包含中文
select * FROM test
WHERE length(name) > char_length(name);
```