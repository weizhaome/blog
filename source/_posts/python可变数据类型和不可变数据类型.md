title: python可变数据类型和不可变数据类型
author: weizhao
date: 2019-09-25 09:16:45
tags:
---
# Python的可变数据类型和不可变数据类型：
## 可变数据类型：  
list：数组是有序的，dict:字典是无序的，多次print一个数组得到的字典顺序可能不一样，可变的set：集合是无序不重复的。Python在声明可变类型后再次声明同样内容的可变类型时，Python会重新申请空间对其进行存储。例如：a=[1,2,3],b=[1,2,3],a is b False， a==b True。is可以用来判断两个变量是否指向同一地址，”==“来判断两个变量的值是否相等。”=“是赋值操作，当a=b时，a,b指向的是同一地址，改变a的值，b的值也会发生变化。
## 不可变数据类型：
string,数值类型，元祖：有序的，不可变set.Python在声明不可变数据类型时会在已经声明的不可变类型对象中找该对象是否已经被声明过，如果已经声明过则变量会直接指向该对象，不会再申请新的内存空间。相当于增加了对象的引用。