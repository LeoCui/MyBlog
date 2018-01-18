---
title: c语言字符串处理函数
date: 2017-08-24 22:19:04
tags:	
	- c/c++
categories: c/c++
---
* c语言中虽然没有c++中那么多字符串处理函数，但是其实有很多都不用我们重复造轮子。
* strtol:  
	* 字符串转整数
* sprintf()
	* 格式化读入数据到字符串中，用好了很神奇，比如：

```
	sprintf(str,"%02x-%02x",sum1,sum2);
	//将sum1,sum2转换成16进制并且存入str
```
* snprintf()
	* 同sprintf,加了长度防止越界
* fprintf()
	* 格式话读入数据到文件流中
* strncpy()
	* 复制n个字符，不够n个后面填充0
* strstr:
	* 求是否包含子串，用来处理经常遇到的abc=123,将abc和123分别存入两个字符串中
	
	```
	char str[]="abc=123";
	char str1[10],str2[10];
	char* p=strstr(str,"=");
	if(p==NULL){
		return;
	}
	int len1=p-str;
	strncpy(str1,str,len1);
	str1[len1]='\0';
	strncpy(str2,len1+1,10);
	```
* sscanf:
	* scanf,sscanf,fscanf中，空格都是分割符，%s,%d后面匹配的时候遇到空格都会停止。%后面是正则却不会停止。
	* 一个非常强大的函数，作用是从一个字符串中提取想要的子串，支持正则表达式，用好了的话非常强大。[参考资料](http://blog.csdn.net/jackyvan/article/details/5349724)
	* 读取配置文件(以空格为分割符): "abc  123"
	
	```
	char str[]="abc 123";
	char str1[10],str2[10]; 
	sscanf(str,"%s%s",str1,str2); 
	//%s可以换成%d,自动完成str to int的转换
	```
	* 读取配置文件(不以空格为分割符): "abc=123"
	
	```
	char str[]="abc=123";
	char str1[10],str2[10];
	// %[^=]表示遇到=就停止写入
	sscanf(str,"%[^=]=%s",str1,str2);
	```
	* 提取某个子串:  "abcd/1345@789",提取/和@之间的部分
	
	```
	char str[]="abcd/1345@789";
	char str1[10],str2[10];
	sscanf(str,"%*[^/]/%[^@]",str1);
	//%*[^@]表示遇到@就停止但是不写入
	```
* fscanf:
	* 用于从文件中解析有规律的字符串，和sscanf类似，只不过来源变成了文件流。
* scanf:
	* 和sscanf类似，只不过第一个参数来源变成了用户的输入