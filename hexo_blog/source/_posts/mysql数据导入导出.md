---
title: mysql数据导入导出
date: 2017-05-29 23:31:51
tags: mysql
categories: Linux
---
* mysql 导出数据到文件: 
mysql -h 10.38.26.21 -P 5100 -uwangguoqiang01 -pabH6j2HUQ7 media -e "select id from app order by id desc limit 10" > export.log
导出数据,文件名不能加引号

* mysql导入数据到数据库：load data local infile "./BadCase2.data" into table org_info character set gbk;

* mysql导出sql语句到文件中：mysqldump -h10.38.26.21 -P5100 -uwangguoqiang01 -pabH6j2HUQ7 media app --skip-lock-tables > test.txt
