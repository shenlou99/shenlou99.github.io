---
title: C#基础操作（十）——枚举
date: 2023-01-24 19:49:20
tags: C#
---

枚举是一组命名整型常量。枚举类型是使用 **enum** 关键字声明的。

C# 枚举是值类型。换句话说，枚举包含自己的值，且不能继承或传递继承。

## 声明 *enum* 变量

声明枚举的一般语法：

```C#
enum <enum_name>
{ 
    enumeration list 
};
```

其中，

- *enum_name* 指定枚举的类型名称。
- *enumeration list* 是一个用逗号分隔的标识符列表。

枚举列表中的每个符号代表一个整数值，一个比它前面的符号大的整数值。默认情况下，第一个枚举符号的值是 0。例如：

```C#
enum Days { Sun, Mon, tue, Wed, thu, Fri, Sat };
```

## 实例

下面的实例演示了枚举变量的用法：

```
using System;

public class EnumTest
{
    enum Day { Sun, Mon, Tue, Wed, Thu, Fri, Sat };

    static void Main()
    {
        int x = (int)Day.Sun;
        int y = (int)Day.Fri;
        Console.WriteLine("Sun = {0}", x);
        Console.WriteLine("Fri = {0}", y);
    }
}
```

当上面的代码被编译和执行时，它会产生下列结果：

```
Sun = 0
Fri = 5
```

**注意：**

和结构体一样，与C语言不同的是，C语言的枚举仍然是作为关键字，在声明（实例化）的时候依然是以（ enum 枚举名 {枚举元素1，枚举元素2，·······} ）作为关键字声明变量，例如：enum book book1;

而C#中是把enum当成类，定义即声明，即（ enum 枚举名 {枚举元素1，枚举元素2，·······} ）此时就已经实例化了，枚举名就是对象，如要选取枚举中的枚举元素，只要对象.枚举元素就可以取出。例如：enum Day { Sun, Mon, Tue, Wed, Thu, Fri, Sat };	取出元素：Day.Sun
