---
title: 几种web服务器
date: 2017-11-16 00:05:01
tags:
	- nginx
	- tomcat
	- apache
	- jvm
categories: 计算机基础
---
* 之前也算做过一点web开发，一直对nginx,apache,tomcat在高并发，多进程下的原理不太了解，现在终于搞清楚一些了。
	* nginx,apahe属于一类，都属于静态服务器，适合展示静态资源。对于动态请求，通常要靠php，python等cgi程序。真正处理用户请求的是cgi程序。一个用户请求就会开一个php进程（类似php index.php这样）。
	* tomcat是动态服务器，tomcat本身就是一个java程序，一个java程序对应一个jvm,一个jvm就是一个进程。所以tomcat只有一个进程，每个请求会在jvm开一个线程来处理。
	* nginx,apache的区别：
		* nginx本身有1个master进程，4个worker进程（cpu核数），nginx内部用了epoll，一个进程处理多个socket连接，实现高并发。(当该进程在等待某个cgi程序的处理结果时，不能让它阻塞在这里，而是注册一个回调函数，然后去接收新的socket连接)一般用来做反向代理，负载均衡。
		* apache给每个连接都开一个进程。
* epoll是实现io复用的一种方法，目的是在一个进程中处理多个socket连接。玩法：

```
while(1){
	events=epoll_wait();    //内核去轮询
	for(event: events){
		if(事件被触发){
			event.callback()
		}
	}
	accept();  // epoll中加入新的socket
}

```
* mq消息队列
	* 典型用法：用于进程或者服务间通信，还可以共享消息，一个生产者可以对应多个消费者。比如有多个service,service1,service2,service3。service1对数据库的某个改动影响到了service2,3。不用消息队列的话，service2，3需要提供一个接口，当service1改动的时候调用这2个接口，但是这样很不优雅而且耦合太大。用了消息队列的话就可以将这个改动push到消息队列，谁用谁自己去取。

* test