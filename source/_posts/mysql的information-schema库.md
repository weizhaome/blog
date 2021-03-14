title: mysql的information_schema库
author: weizhao
date: 2021-03-14 20:55:40
tags:
---
# information_schema数据库中保存了mysql服务器所有数据库的信息。如：数据库名、数据库表、表的列名、访问权限等。

* information_schema的表schema中的列schema_name记录了所有数据库的名字。
* information_schema的表tables中的列table_schema记录了所有的数据库名字。
* information_schema的表tables中的列table_name记录了所有数据库的表的名字。
* information_schema的表columns中的列table_schema记录了所有的数据库名字。
* information_schema的表columns中的列table_name记录了所有数据库表的名字。
* information_schema的表columns中的列columns_name记录了所有数据库表的列的名字。