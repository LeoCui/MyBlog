---
title: 'c++基础,长期更新'
date: 2016-10-20 19:05:04
tags: 
  - c/c++
categories: c/c++
---

   今天在写操作系统的作业，发现c++的很多基本语法都忘了，现在自己把基本语法总结一遍。方便以后复习。
   
   1.构造函数：
     父类构造函数 -> 类成员的构造函数 -> 自己的构造函数
     
   2.初始化列表：
     这里有个博客挺好       http://www.cnblogs.com/graphics/archive/2010/07/04/1770900.html
     
   我的总结：
 
``` c++
Test1 test1 ;
    Test2(Test1 &t1):test1(t1){}

```

```
 Test1 test1 ;
    Test2(Test1 &t1)
    {
        test1 = t1 ;
    }

```

第2种test1需要执行一次默认构造函数+一次赋值操作
第1种test1只需要执行一次拷贝构造函数

特别的：下面情况只能用初始化列表
*  类成员没有默认构造函数
*  类成员是引用类型（只能初始化，不能赋值）
*  类成员是常量（只能初始化，不能赋值）
* 多个初始化列表，不是按初始化列表顺序，而是按声明顺序

结论： 尽可能用初始化列表

初始化列表顺序和声明顺序一致


3.extern 外部的，extern 只是起一个declare作用，可以用来修饰变量和函数，表示该函数的定义在其他模块中，也就是说，如果你在a.cpp文件中定义a=1;在b.cpp文件中声明extern  a;则可以引用a.cpp中的a。

4.#ifdef表示条件编译

5.#define 和 typedef的区别：
define预处理，无脑替换
typedef是别名，不一样。
define  INT  int*
typedef  int*  INT
则 INT  a,b:
typedef:   int* a,b:  a,b都是int*
define:   int*a,b  : a是int*，b是int
		
5.类的定义 

* 关于默认构造函数(没有参数)，如果类中未定义任何构造函数，编译器会提供一个默认的构造函数，**如果类中定义了任何了构造函数，编译器不会提供默认构造函数。

``` 
class Test{                                                                           
	int a;               
	int b;     
	Test(int a,int b){
	
	} 
	Test(){
	
	}
}
```
* 局部变量： Test  a1; Test a2(1,2);    
如果调用默认构造函数，不用加括号；
* new 对象：Test* p1=new Test(), *p2=new Test(10,20);     
必须加括号，调用默认构造函数也要加括号
* 匿名对象：vector.push\_back(Test()),                   
vector.push\_back(Test(10,20))      
必须加括号
* 关于lambda表达式：我觉得可以理解成一个匿名函数，通常用到需要传递函数指针做参数，而函数本身又比较简单的情况，比如sort函数的cmp函数。
	* 格式： [capture list]（parameter list）-> return type {function body} 
		* capture list: 捕获列表,一般为空，表示可以在lambda表达式中用所在函数中局部变量的值。如[a,&b]表示捕获a,b其中b为引用。当然还有其他的隐式捕获的用法，具体见c++ prime page 352
		* parameter list: lambda的参数
		* return type: 需要注意的是，如果函数体内只有一句return语句，则可以省略return type; 否则默认返回类型是void，如果返回的不是void，则需要加上具体的返回类型。
	* 例子：
	
	```
	sort(vector1.begin(),vector1.end(),[](int a,int b)->bool{return a>b})
	```
* c++的STL中的类型不能为引用，如vector<int&>是绝对错误的