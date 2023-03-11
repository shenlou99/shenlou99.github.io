---
title: C语言标准库——va_list
date: 2023-03-11 15:41:21
tags: va_list
categories: C语言标准库
---

## 一、定义

va_list是在C语言中解决变参问题的一组宏，所在头文件：**#include<stdarg.h>**，用于获取不确定个数的参数。

## 二、意义

当你的函数的参数个数不确定时，就可以使用上述宏进行动态处理。

## 三、使用方法

- 首先在函数中定义一个具有va_list型的变量，这个变量是指向参数的指针。
- 然后用va_start() 宏初始化变量刚定义的va_list变量，使其指向第一个可变参数的地址。
- 然后va_arg返回可变参数，va_arg的第二个参数是你要返回的参数的类型（如果多个可变参数，依次调用va_arg获取各个参数）。
- 最后使用va_end宏结束可变参数的获取。

## 四、注意点

在使用va_list时应该注意以下问题：

- 可变参数的类型和个数完全由代码控制，它并不能智能地识别不同参数的个数和类型。
- 如果我们不需要一一详解每个参数，只需要将可变列表拷贝到某个缓冲区，可以用vsprintf函数。
- 因为编译器对可变参数的函数原型检查不够严格，对编程查错不利，不利于我们写出高质量的代码。

## 五、示例

```C++
#include "stdarg.h"
#include <iostream.h>

int sum(char* msg,...);

int main()
{
	int total = 0;
	total = sum("hello world",1,2,3);
	std::cout << "total = " << total <<std::endl;
	system("pause");
	return 0;
}

int sum(char* msg,...)
{
	va_list vaList;	//定义一个具有va_list型的变量，这个变量是指向参数的指针。
	va_start(vaList,msg);	//第一个参数指向可变列表的地址，地址自动增加，第二个参数为固定值
	std::cout << msg << std::endl;
	int sumNum = 0;
	int step;
	while((step = va_arg(vaList,int)) < 4)	//va_arg第一个参数是可变参数的地址，第二个参数是传入参数的类型，返回值就是va_list中接着的地址值，类型和va_arg的第二个参数一样。
        //不等于0表示，va_list中还有参数可取
	{
        //va_arg取得下一个指针
		sumNum += step;
	}
	va_end(vaList);		//结束可变参数列表
	return sumNum;
}
```

运行结果：

hello world

total=6
