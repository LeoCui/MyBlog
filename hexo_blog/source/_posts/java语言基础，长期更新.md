---
title: java语言基础，长期更新
date: 2016-10-20 20:30:57
tags:  java
categories: java
---


0.eclipse操作技巧：ctrl+变量： 查看定义 
ctrl+7 批量注释

1.命名规范： 
包名：  cuiyiming
类名/变量名：  CuiYiMing
方法名：cuiYiMing
常量名：CUI_YI_MING

2.大括号： 第一个不换行

2.main 函数： 
只能是 public static void main(String[] args)形式，public 表示函数可以访问，static 表示 属于这个类，不需要new 对象,void 表示没有返回值，因为不知道返回值给谁。所以强制规定没有。

3.import 类似于c#中的namespace,逻辑上对类进行组织和管理。

4.java 访问权限: 
public protected default private 
修饰类：public default 
修饰成员变量和函数： public protected default private 
判定一个函数能否访问，先通过类修饰符，再通过函数修饰符，两重判定 
![这里写图片描述](http://img.blog.csdn.net/20151104220756295)

5.static :静态量，属于类，存在静态存储区，编译时分配内存。 
特点：静态方法只能调用静态变量。
原因：非静态量调用时必须要有this指针，但是静态方法显然不能为他提供this 指针。
