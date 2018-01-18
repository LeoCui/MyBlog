---
title: Linux/Windows环境变量那些事
date: 2016-04-11 20:17:39
tags: 
  - 环境变量
  - Linux
categories: 操作系统
---
变量：相当于别名，举个例子：linux 中，HOME就是一个变量，它一般指的是/home/leo,leo是我的用户名。   
变量名不能单独出现,必须加上 “美元符”(linux)
或%%(windows)表示引用它的值。   
在linux中:   可以通过echo $HOME查看变量的值   
在windows中： echo %HOME%

环境变量：path ,path实质上是一种特殊的变量。它等于一系列路径（windows用;隔开,linux用：隔开）。   
Linux的命令实质上就是在执行程序，执行程序时，系统会到当前目录寻找程序路径，找不到就到环境变量对应的路径中去寻找              
环境变量的作用是当执行或者链接某个程序的时候，不需要切换到具体的目录下在执行。

顺便说一下：命令行中执行某个程序，只要写出路径即可，之前我还一直以为./是执行的意思呢，真是too young!!
update:今天才发现要想执行某程序：   
1.输入完整路径 如/home/leo/test   
2.输入当前目录 ./test ,在当前目录下只输入test 是不行的。  
3.只输入文件名，这种要求必须设置环境变量


那么怎么设置环境变量呢？
windows:  直接搜索“环境变量”，在path路径下添加要添加的目录(不要忘记;)
linux下，在/etc下找到profile文件，用gedit 打开，export PATH=自己路径：$PATH，保存


linux还有一个命令：alias
alias看起来仿佛跟变量很像，其实是不同的。alias可以看成是一种批处理，它可以将一个或多个命令重命名为一个命令。
alias:  查看alias内容
alias  test="cd /home;ls;" ，可以将一系列命令命名成一个。(临时命名，当前窗口有效)   
如果想永远命名：在home/leo中找到.bashrc文件，然后找到alias部分，添加自定义命名，如alias  test="cd /home;ls;" 
那么可能有人问？怎么在windows中实现alias呢，可以通过批处理实现。举个例子，在windows中想用ls,就可以创建ls.bat,内容为dir. 然后ls就可以用了。    
tips:  alias 后面可以跟参数。
bat文件后面好像不可以跟参数。


