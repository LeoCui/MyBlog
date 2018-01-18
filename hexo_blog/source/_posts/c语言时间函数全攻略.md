---
title: c语言时间函数全攻略
date:  2016-4-10 19:13:32
tags:  
  - 时间函数
  - c语言
  - Linux
categories: c/c++
---

最近在做操作系统相关的实验，其中经常用到获取系统的时间等函数，现在总结一下。

概念：gmt: GreenWich mean time          //格林威治时间
          
 utc:   Coordinated universal time //世界时
            格林威治时间由本初子午线有关，但是现在发现不太精确，不再使用。
            utc时间由原子钟确定，更加精确，现在表达时区一般这样表达，如北京utc-8。

通用的库:time.h>      
   
struct____tm{ year,month,....second
} // month[0,11], year=now-1900  
time_______t: (long int)                                                  
time_______t* time(NULL): 获得1970年1月1日到现在的秒数，utc时间   
char * ctime(time_______t*):将time_____t转换成字符串,gmt时间      
struct tm* localtime(time______t):utc秒数变成当地时间(时区)      
struct tm* gmtime(time______t):utc秒数变成gmt时间      
综上：time()得到的秒数是确定的，区别就是转换成具体时间是gmt时间还是当地时间，直接由time__t计算,不加时区得到的是gmt时间


    特有的类：Linux 下：
        <sys/time.h>    
        strcut timeval ，struct timezone
        struct timeval{
	       second;      //应该都是long int
	       u second;    // 微秒
        }
        timezone: 存储时区信息
        gettimeofday(struct timeval*,struct timezone*)


    windows下：
        <windows.h> GETSYSTEMTIME,SYSTEMTIME
        SYSTEMTIME: year,month,...second, msecond,  毫秒
        GETSystemTime(SYSTEMTIME*)    //utc
        GETLocalTime(SYSTEM*)         //local

综上：如果想写跨平台通用的:
time+ctime 就够了，不能精确到ms       
精确到ms：windows+getsystem就够了      
linux下：   gettimeofday -> timeval ->time__t -> getime -> struct tm,麻烦一点。

顺便说下                                                                                                        sleep函数：    
windows:   
sleep()  //parament 是 s   
Sleep()                 //parament 是 ms,毫秒   

Linux:
sleep( ) //parament 是 s     
usleep()  //单位是 us ，微秒

1s= 1000 ms =1000000 us




                    
