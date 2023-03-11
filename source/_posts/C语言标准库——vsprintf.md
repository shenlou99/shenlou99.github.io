---
title: C语言标准库——vsprintf
date: 2023-03-11 16:46:16
tags: vsprintf
categories: C语言标准库
---

## 一、定义

vsprintf是C语言库函数之一，属于可变参数。用于向字符串中打印数据、数据格式用户自定义。

头文件是：**#include “stdarg.h"**

**函数声明：**

int vsnprintf(char* str,size_t size,const char* format,va_list ap);

**参数说明：**

char* str[out]：把生成的格式化的字符串存放在这里。

size_t size：str可接受的最大字符数（**非字节数**）。注意防止数组越界！

const char* format：指定输出格式的字符串。

va_list ap：va_list变量。

**函数功能：**

将可变参数格式化输出到一个字符数组。

**返回值：**

执行成功，返回最终生成字符串的长度，若生成字符串的长度大于size，则将字符串的前size个字符复制到str，同时将原串的长度返回（不包含终止符）；

执行失败，则返回负值，并置errno。

## 二、示例

```C
#include "stdio.h"
#include "stdarg.h"

void PrintFError(const char* format,...)
{
	char buffer[256];
	va_list args;
	va_start(args,format);
	vsnprintf(buffer,256,format,args);
	perror(buffer);
	va_end(args);
}

int main()
{
	FILE* pFile;
	char szFileName[] = "myfile.txt";
	pFile = fopen(szFileName,"r");
	if(pFile == NULL)
	{
		PrintFError("Error opening '%s'",szFileName);
	}
	else
	{
		fclose(pFile);
	}
	return 0;
}
```



