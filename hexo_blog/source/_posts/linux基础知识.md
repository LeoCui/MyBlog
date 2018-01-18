---
title: linux基础知识
date: 2016-11-14 20:39:07
tags: linux
categories: Linux
---



```
文件的类型					linux				windows

二进制文件					.o  				.obj
静态链接库					.a  				.lib
动态链接库					.so 				.dll
可执行文件					.out				.exe
文件的格式					ELF 				PE

//二进制文件有叫目标文件，每个.c文件编译后产生的
//静态链接库是很多目标文件的集合

```

* linux可执行文件结构: elf, windows:PE ,macos: mach-o    
(值得注意的是，压缩文件在mac上先解压在压缩后在linux下再解压就打不开了,所以copy一般都是tar.gz文件)
* 有时程序显示无法load  .so 文件,跟环境变量无关，系统加载环境变量一般在/usr/lib中找，如果要改的话      
1.将so文件移到/usr/lib中。   
2.设置软链接，链接到/usr/lib中     
3.修改/etc/ld.so.conf文件，加入自己的路径

* gcc编译命令：
	* -c 只编译，不链接，生成.o
	* -o 生成目标文件，加上-c生成的就是只编译后的目标文件,不加-c生成的就是编译+链接后的目标文件,.o,.so,.a,.out都是目标文件。
	* -fPIC 一般都加上
	* 生成.o:  gcc -c test.c
	* 生成.so: gcc -shared -o test.so test.c
	* 生成.a: gcc -o test.a test.c
	* 生成.out: gcc -o test.out test.c
	* 调用动态库：-lpthread -ldnet(glic的库），gcc test.c ./test1.so 直接一起编译
  