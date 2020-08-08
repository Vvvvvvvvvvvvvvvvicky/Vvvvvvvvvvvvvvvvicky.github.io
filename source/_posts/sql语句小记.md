---
title: SQL语句小记
date: 2018-05-14 18:42:23
tags: SQL 
categories: 学习 
comments: true 
---

记录常用SQL语句。

<!--more-->

##### 1.为表中字段添加唯一约束

alter table TABLE_NAME add unique key (COLUMN_NAME); 

##### 2.为表中字段添加联合唯一约束

alter table TABLE_NAME add unique key (COLUMN_NAME_1, COLUMN_NAME_2) ;

##### 3.可变长度类型的字段设置索引，需要限制长度（前n个）

alter table TABLE_NAME add unique key (COLUMN_NAME_1, COLUMN_NAME_2(255))；