---
title: gdb命令总结
date: 2016-11-03 18:35:50
tags: gdb命令
categories: Linux
---

* list+行号(函数名)：查看某一行(函数)的代码
* break+file.c:行号: 在某个文件设置断点，如果只有一个文件则不需要
* 条件断点：break test.c:34 if count>50,一般用在循环中设置断点
* start: 停在main函数第一条
* run(r):   开始运行，停在断点处
* continue(c): 继续运行，停在下一个断点
* next(n): 单步执行
* until+行号: 继续运行，直到某一行停止
* p :  查看变量
* step(s): 进入函数
* quit(q): 退出gdb
* info threads: 显示所有线程信息
* gdb调试带参数的程序如main： gdb main ，r a b c ，abc为参数
* bt: backtrace,打印当前的函数调用栈信息
* ctrl+a+x: 上方显示源代码，下方gdb调试