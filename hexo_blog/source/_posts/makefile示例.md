---
title: makefile示例
date: 2017-08-24 21:32:50
tags: 
	- makefile
	- c/c++
categories: c/c++
---

```
CC = gcc
TARGET_DIR = ../../mysapp/plug/business/live_monitor
TARGET_CONF_DIR = ../../mysapp/conf/live_monitor
TARGET = live_monitor.so
INF = ../bin/live_monitor.inf
CONF = ../conf/live_list.csv
CFLAGS = -g -Wall -fPIC
LIB = -lpthread
LIB += -lMESA_handle_logger
LIB += -lMESA_prof_load
LIB+= -lMESA_htable
INCLUDES = -I./inc/
INCLUDES += -I/usr/include/MESA
SOURCES = $(wildcard *.c)
OBJECTS = $(SOURCES:.c=.o)
DEPS = $(SOURCES:.c=.d)
.PHONY : clean all install
all : $(TARGET)
$(TARGET) : $(OBJECTS)
	$(CC) $(CFLAGS) -shared -o $(TARGET) $(LIB) $(OBJECTS)
%.o : %.c 
	$(CC) $(CFLAGS) -c $< -o $@
%.d : %.c
	$(CC) $< -MM $(INCLUDES) > $@ 
-include $(DEPS)
clean : 
	-rm $(TARGET) $(OBJECTS) $(DEPS) ../bin/$(TARGET)
	-rm -rf $(TARGET_DIR)
	-rm -rf $(TARGET_CONF_DIR)
install : 
	-mkdir $(TARGET_DIR)
	-cp $(TARGET) $(TARGET_DIR)
	-cp $(TARGET) ../bin
	-cp $(INF) $(TARGET_DIR)
	-mkdir $(TARGET_CONF_DIR)
	-cp $(CONF) $(TARGET_CONF_DIR)
```
* makefile的执行过程：其实make clean,make install都是我们定义的，make x,makefile就会去找x，然后根据依赖文件一步步找下去。
* wildcard *.c:当前文件夹中所有的.c文件
* $(SOURCES: .c=.o):将.c都变成.o
* .d文件存的是每个.c文件依赖的.c文件,-include $(DEPS)不能少
* $<和$@都是临时变量
* .PHONY的作用：定义一个伪目标，保证这条命令一定会被执行。如果不加的话，比如make clean,由于clean没有依赖文件，如果当前目录中存在一个文件叫clean，那么clean后面的语句就不会执行。