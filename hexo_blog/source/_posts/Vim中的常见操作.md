---
title: Vim中的常见操作
date: 2017-01-01 19:24:10
tags:
  - Vim
categories: Vim
---

* 几种模式
	* Normal模式：按Esc进入
	* Insert模式：按i进入
	* Visual模式：按v进入
* Vim 中复制粘贴：
	* 选中，然后右键，这种缺点会将行号也复制进去
	* Visual模式下，用上下箭头选中，然后按y复制，按p粘贴
	* Normal模式下，输入row1,row2+y，表示复制从row1到row2的行，然后找到指定位置按p粘贴

* vim 中复制粘贴（简单方法）
	* yy + p :复制一行粘贴
	* set mouse=v : 然后选择即复制，可以在任何地方粘贴（强烈推荐）
* set paste:解决从其他地方粘贴过来乱码的问题
* dd: 删除某一行
* G: 跳到末尾，gg:跳到开头
* fn+home:跳到一行开头
* fn+end: 跳到一行末尾
* %s/word1/word2/g:批量将word1替换成word2,%表示全文搜索，g表示全文替换，转义字符是\
* set mouse=*: 表示只在 * 模式下使用鼠标功能。使用鼠标功能的话vim的光标会随着鼠标移动，但是缺点是无法复制。默认情况下set mouse=a，无法复制。set mouse=v的话，也就是只在v模式下使用鼠标功能，其他模式下则可以右键复制。

* 批量缩进： visual模式下 > <号