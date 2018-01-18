---
title: Windows/Linux进程控制实验
date: 2016-04-11 20:11:16
tags: 
  - 操作系统
  - 进程控制
  - Linux
categories: 操作系统
---

最近做了操作系统的实验，进程控制，踩了不少坑。现在总结下。
Liunx：先放代码

```
#include<iostream>
#include<cstdlib>     //sleep()
#include<unistd.h>    //fork
#include<sys/time.h>  //gettimeofday
#include<sys/wait.h>  //wait
#include<ctime>       //localtime
void outputTime(struct tm*time,int ms);
using namespace std;
int main(int argc,char*argv[])
{
    struct timeval startTime;
    struct timeval endTime;
    struct timezone zone;
    time_t startTime_t;
    time_t endTime_t;
    struct tm *startTime_tm;
    struct tm *endTime_tm;
    int pid=fork();
    if(pid<0){
        cout<<"error"<<endl;
        exit(0);
    }
    if(pid==0){   //子进程
        execvp(argv[1],NULL); 
	cout<<"execv error!"<<endl;
	exit(0);
    }
    if(pid>0){    //父进程
        gettimeofday(&startTime,&zone);
        wait(0);   //等待子进程结束
        gettimeofday(&endTime, &zone);
        long long int durtion=(endTime.tv_sec-startTime.tv_sec)*1000+endTime.tv_usec-startTime.tv_usec;
        startTime_t=(time_t)startTime.tv_sec;  //转换成time_t格式
        endTime_t=(time_t)endTime.tv_sec;
        startTime_tm=localtime(&startTime_t);  //转换成struct tm格式
        endTime_tm=localtime(&endTime_t);
        cout<<"The start time is:  ";
        outputTime(startTime_tm,startTime.tv_usec/1000);
        cout<<"The end time is:    ";
        outputTime(endTime_tm,endTime.tv_usec/1000);
        cout<<"the durtion is "<<durtion<<"ms"<<endl;
    }
    return 0;
}

void outputTime(struct tm*time,int ms){
    cout<<(*time).tm_year+1900<<"/"<<(*time).tm_mon+1<<"/"<<(*time).tm_mday<<"  "<<(*time).tm_hour<<":"<<(*time).tm_min<<":"<<(*time).tm_sec<<":"<<ms<<endl;
}

```
几个坑：   
1.之前一直不知道主函数要什么参数，这下知道了。主要是在命令行运行中可能需要传入参数。比如启动一个子进程。     
2. 每个函数对应的头文件要搞清楚。    
3.execvp: exec类的函数都是杀死现有进程，用新进程代替，进程号不变。但是execvp()，可以识别环境变量，其他不可以。换句话说：如果传入参数是有环境变量的，而且用的是execvp()，那么只传函数名是可以的。两个条件缺一不可。   
4.wait(0)可以，wait(NULL)本来应该是可以的，但是不知道为什么在linux中不可以。


windows:

```
#include<iostream>
#include<string>
#include<windows.h>
using namespace std;
void  outputTime(SYSTEMTIME&time);
int getDurtion(SYSTEMTIME&startTime, SYSTEMTIME&endTime);
int main(int argc, char* argv[]) {               //L表示unicode编码，c++和java不同，内部可能有几种编码，烦。。
	SYSTEMTIME startTime;   //LP表示指针的意思
	SYSTEMTIME endTime;     
	GetSystemTime(&startTime);
	STARTUPINFOA si;  //后面有A表示char,否则是wchar
	PROCESS_INFORMATION pi;
	memset(&si,0, sizeof(si));         
	si.cb = sizeof(STARTUPINFO);
	si.dwFlags = STARTF_USESHOWWINDOW;  // dwflags参数表明子进程是否用wshowWindow这个参数
	si.wShowWindow = TRUE;           // 当创建一个进程，wshowWindows作为参数传递给main函数,true 表示显示子进程的窗口
	bool flag=CreateProcessA(NULL,argv[1], NULL, NULL, FALSE, CREATE_NEW_CONSOLE, NULL, NULL, &si, &pi);
	if (flag) {                  //createProcessA表示第二个参数是char[],createProcess表示wchar[](unicode)
		GetLocalTime(&startTime);
		WaitForSingleObject(pi.hProcess, INFINITE);  //等待子进程结束
		GetLocalTime(&endTime);
		int durtion = getDurtion(startTime, endTime);
		cout << "The start time is: ";
		outputTime(startTime);
		cout << "The end time is:   ";
		outputTime(endTime);
		cout << "The durtion is " << durtion << "ms" << endl;
	}
	else {
		cout << "The chiidProcess failed to be created!!";
	}
	getchar();
}
void  outputTime(SYSTEMTIME&time){
	cout << time.wYear << "/" << time.wMonth << "/" << time.wDay << "  " << time.wHour << ":" << time.wMinute <<
		":" << time.wSecond << ":" << time.wMilliseconds<<endl;
}
int getDurtion(SYSTEMTIME&startTime, SYSTEMTIME&endTime) {
	int tempHour = endTime.wHour - startTime.wHour;
	int tempMinute = endTime.wMinute - startTime.wMinute;
	int tempSecond = endTime.wSecond - startTime.wSecond;
	int tempMillSecond = endTime.wMilliseconds - startTime.wMilliseconds;
	int duration = ((tempHour * 60 + tempMinute) * 60 + tempSecond) * 1000 + tempMillSecond;
	return duration;
}
```

几个坑：        
1.编码：c++ 编码是乱的，没有一个统一的编码，有char,wchar 涉及到中文的时候就很容易出错。   
解决方法：createProcessA(),STARTUPINFOA,这样就都是char,路径也别设成中文就可以。  
2. 配环境的时候，经常缺头文件，需要找到头文件的目录，然后将其添加到path 中就可以。   
lib: 库文件，具体实现   
include: 头文件，声明和定义     
3.手动编译：cl  test.cpp   
编译命令：
gcc,g++: 是linux
microsoft: cl