---
title: python基本用法
date: 2018-01-06 15:23:01
tags: python 
categories: python
---
* import
	* module和package:
		* module是一个.py文件，导入一个module就是把这个python文件加载进内存
		* package是一个文件夹，必须有\_ \_init\_ \_.py文件,导入一个package就是将\_ \_init\_ \_.py加载进内存，并且import package的时候自动执行\_ \_init\_ \_.py文件
	* import 机制
		* import导入的所有包都在sys.modules中
		* from A import B，导入一个包或者模块中的部分文件或者函数
	* 绝对导入和相对导入：
		* 绝对导入：
			* 搜索路径： sys.path()
			* 如果直接python test.py,那么test.py的路径是在sys.path中的
			* 如果想搜索某个module或者package，只需将其所在文件夹的路径加入sys.path即可：sys.path.append()
			* 获取当前python文件路径：
				* pwd = os.getcwd()
				* pwd = os.path.dirname(pwd)
		* 相对导入：
			*  形如from .. import x
			*  在python3中，找到当前目录是通过\_name\_，特别地，如果直接python执行某个python文件，那么\_name\_就是\_main\_,那么当前目录就是顶层目录
			*  如果\_name\_是A.B.C说明当前目录为B,那么from .. 的路径就是A，from . 就是B 