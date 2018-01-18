---
title: linux命令
date: 2016-10-24 14:26:22
tags: linux命令
categories: Linux
---
### 查用法： man+命令(man中搜索用/,vim同)
* 读懂man 命令：--跟单词，-跟字母，[]表示可选，[-z,--gzip]实际上是一个参数，不同写法。
#####  grep: golbal search regular expression and print

* 查看版本信息： lsb_release -a
* /表示根目录，~表示HOME目录
* 复制文件夹  ： copy -r
* 查看端口占用情况 ： netstat -antp | grep 8080
* 查看网卡对应网络：networksetup -listallhardwareports
* 查看进程占用信息： top
* 杀死某进程 ：  kill -9 pid
* 打包压缩： tar -zcvf test.tar.gz /temp
* 解压：  tar -zxvf test.tar.gz
* 查看进程信息 ： ps -ef | grep ""
* 全盘搜索某文件：  locate+文件名
* 设置软链接  ：ln -s src  dst(必须完整路径，如ln -s /home/a.cpp /usr/lib/a.cpp),删除按照普通文件处理就行
* 查看动态链接库： ldd+程序名（完整路径，环境变量无效，不知道为什么）
* 查看可执行文件位置： whereis
* 模拟tcp,ip通信神器：nc
* 捕获包：tcpdump
* 搜索历史命令： ctrl+r
* 搜索指文件夹中的字符串： grep -rn keyword ./   表示递归搜索当前目录下的所有文件
* 远程传送文件：scp  -P port file root@ip:/home/
* 远程登录： ssh root@ip -p port,如果不想每次都输入密码，可以配置一下公钥登录，[具体教程](http://chenlb.iteye.com/blog/211809)
* 退出ssh：exit
* 追加文件：cat file1>>file2  将file1追加到file2
* 构造自己的命令：alias str='command1;command2',多条命令依次执行的时候，&&遇到错误会停止，;遇到错误会跳过
* grep -r " " ./ --color:搜索文件内容，将搜出来的内容标红
* find ./ -name test.c: 递归查找文件或文件夹 
* tail -f file：监控文件的输出
* ctrl+a :光标移到行首
* ctrl+e:光标移动到行尾
* wc -l:统计文件函数，常用来配合|管道命令来用
* sed: 批量替换文件
* git diff file1 file2:diff两个文件
* awk: 强大的文件处理工具,会将文件按照分行，并且每一行按照空格分开，如awk '{print $14; print $4}' data.20170516 | less.表示分行输出每一行的第4个和第14个变量。
* chown:change owner,改变文件的所有者。 
	* sudo chown -R $(whoami) ./ 将当前目录的所有文件(递归) 的拥有者都改成当前用户
* chmod: change mode，改变文件的属性(可读，可写，可执行)
	* chmod u+x,g+x,o+x file1，将file1增加可执行权限，u:拥有者，g:用户组，o:其他用户，a:所有用户
	* chmod 777 file2
* sed -n '5,10p' filename: 显示5-10行