---
title: C#基本操作（四）——类型转换
date: 2023-01-24 12:36:00
tags: C#
categories: C#
---

# C# 类型转换

类型转换从根本上说是类型铸造，或者说是把数据从一种类型转换为另一种类型。在 C# 中，类型铸造有两种形式：

- **隐式类型转换** - 这些转换是 C# 默认的以安全方式进行的转换, 不会导致数据丢失。例如，从小的整数类型转换为大的整数类型，从派生类转换为基类。
- **显式类型转换** - 显式类型转换，即强制类型转换。显式转换需要强制转换运算符，而且强制转换会造成数据丢失。

下面的实例显示了一个显式的类型转换：

```c#
namespace TypeConversionApplication
{
    class ExplicitConversion
    {
        static void Main(string[] args)
        {
            double d = 5673.74;
            int i;

            // 强制转换 double 为 int
            i = (int)d;
            Console.WriteLine(i);
            Console.ReadKey();
           
        }
    }
}
```

当上面的代码被编译和执行时，它会产生下列结果：

```c#
5673
```

### C# 类型转换方法

C# 提供了下列内置的类型转换方法：

| 序号 | 方法 & 描述                                                  |
| ---- | ------------------------------------------------------------ |
| 1    | **ToBoolean** 如果可能的话，把类型转换为布尔型。             |
| 2    | **ToByte** 把类型转换为字节类型。                            |
| 3    | **ToChar** 如果可能的话，把类型转换为单个 Unicode 字符类型。 |
| 4    | **ToDateTime** 把类型（整数或字符串类型）转换为 日期-时间 结构。 |
| 5    | **ToDecimal** 把浮点型或整数类型转换为十进制类型。           |
| 6    | **ToDouble** 把类型转换为双精度浮点型。                      |
| 7    | **ToInt16** 把类型转换为 16 位整数类型。                     |
| 8    | **ToInt32** 把类型转换为 32 位整数类型。                     |
| 9    | **ToInt64** 把类型转换为 64 位整数类型。                     |
| 10   | **ToSbyte** 把类型转换为有符号字节类型。                     |
| 11   | **ToSingle** 把类型转换为小浮点数类型。                      |
| 12   | **ToString** 把类型转换为字符串类型。                        |
| 13   | **ToType** 把类型转换为指定类型。                            |
| 14   | **ToUInt16** 把类型转换为 16 位无符号整数类型。              |
| 15   | **ToUInt32** 把类型转换为 32 位无符号整数类型。              |
| 16   | **ToUInt64** 把类型转换为 64 位无符号整数类型。              |

下面的实例把不同值的类型转换为字符串类型：

```c#
namespace TypeConversionApplication
{
    class StringConversion
    {
        static void Main(string[] args)
        {
            int i = 75;
            float f = 53.005f;
            double d = 2345.7652;
            bool b = true;

            Console.WriteLine(i.ToString());
            Console.WriteLine(f.ToString());
            Console.WriteLine(d.ToString());
            Console.WriteLine(b.ToString());
            Console.ReadKey();
           
        }
    }
}
```

当上面的代码被编译和执行时，它会产生下列结果：

```c#
75
53.005
2345.7652
True
```

### 接受来自用户的值

**System** 命名空间中的 **Console** 类提供了一个函数 **ReadLine()**，用于接收来自用户的输入，并把它存储到一个变量中。

例如：

```c#
int num;
num = Convert.ToInt32(Console.ReadLine());
```

函数 **Convert.ToInt32()** 把用户输入的数据转换为 int 数据类型，因为 **Console.ReadLine()** 只接受字符串格式的数据。
