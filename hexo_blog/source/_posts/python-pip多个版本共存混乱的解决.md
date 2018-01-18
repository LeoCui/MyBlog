---
title: 'python,pip多个版本共存混乱的解决'
date: 2017-09-19 17:39:15
tags: python 
categories: Linux
---
* 今天在搞django的时候又被各种python版本共存的问题坑了。记录一下：
* 首先区分两个概念: usr:unix system resource
	* /usr/bin,/usr/lib/,usr/lib64,一般unix系统的软件和lib都在这个里面，yum安装的一般都在这个目录下
	* /usr/local/bin,/usr/local/lib，这个一般非yum安装的软件会放到这个目录下
* 多个版本的python其实比较好解决，用那个设一下软连接就可以了，pip是2的，pip3是3的
* 今天我遇到的这个问题是python3和pip3不匹配，现在我的Python3在/usr/bin下，所以它的模块默认搜索路径是/usr/lib/,/usr/lib64，但是pip3是在/usr/local/bin下的，所以pip3安装的模块都在/usr/local/python3.4/site-packages下，所以就找不到模块
	* 解决办法：yum安装pip3(/usr/bin)下，然后设置pip的软连接到/usr/pip3,这样pip安装的模块就在/usr/lib64/site-packages下了。
