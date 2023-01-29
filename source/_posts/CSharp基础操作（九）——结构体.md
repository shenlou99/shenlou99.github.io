---
title: C#基础操作（九）——结构体
date: 2023-01-24 19:24:35
tags: C#
categories: C#
---

## 定义结构体

为了定义一个结构体，您必须使用 struct 语句。struct 语句为程序定义了一个带有多个成员的新的数据类型。

例如，您可以按照如下的方式声明 Book 结构：

```C#
struct Books
{
   public string title;
   public string author;
   public string subject;
   public int book_id;
};  
```

下面的程序演示了结构的用法：

```C#
using System;
using System.Text;
     
struct Books
{
   public string title;
   public string author;
   public string subject;
   public int book_id;
};  

public class testStructure
{
   public static void Main(string[] args)
   {

      Books Book1;        /* 声明 Book1，类型为 Books */
      Books Book2;        /* 声明 Book2，类型为 Books */

      /* book 1 详述 */
      Book1.title = "C Programming";
      Book1.author = "Nuha Ali";
      Book1.subject = "C Programming Tutorial";
      Book1.book_id = 6495407;

      /* book 2 详述 */
      Book2.title = "Telecom Billing";
      Book2.author = "Zara Ali";
      Book2.subject =  "Telecom Billing Tutorial";
      Book2.book_id = 6495700;

      /* 打印 Book1 信息 */
      Console.WriteLine( "Book 1 title : {0}", Book1.title);
      Console.WriteLine("Book 1 author : {0}", Book1.author);
      Console.WriteLine("Book 1 subject : {0}", Book1.subject);
      Console.WriteLine("Book 1 book_id :{0}", Book1.book_id);

      /* 打印 Book2 信息 */
      Console.WriteLine("Book 2 title : {0}", Book2.title);
      Console.WriteLine("Book 2 author : {0}", Book2.author);
      Console.WriteLine("Book 2 subject : {0}", Book2.subject);
      Console.WriteLine("Book 2 book_id : {0}", Book2.book_id);      

      Console.ReadKey();

   }
}
```

当上面的代码被编译和执行时，它会产生下列结果：

```
Book 1 title : C Programming
Book 1 author : Nuha Ali
Book 1 subject : C Programming Tutorial
Book 1 book_id : 6495407
Book 2 title : Telecom Billing
Book 2 author : Zara Ali
Book 2 subject : Telecom Billing Tutorial
Book 2 book_id : 6495700
```

***注意：***

**C语言：**

##### 一、结构体定义：

格式：

```c
struct tag {    
	member-list    
	member-list    
    member-list     
    ... 
} variable-list ;
```

实例：

1. ```C
   //此声明声明了拥有3个成员的结构体，分别为整型的a，字符型的b和双精度的c
   //同时又声明了结构体变量s1
   //这个结构体并没有标明其标签
   struct 
   {
       int a;
       char b;
       double c;
   } s1;
   ```

2. ```C
   //此声明声明了拥有3个成员的结构体，分别为整型的a，字符型的b和双精度的c
   //结构体的标签被命名为SIMPLE,没有声明变量
   struct SIMPLE
   {
       int a;
       char b;
       double c;
   };
   //用SIMPLE标签的结构体，另外声明了变量t1、t2、t3
   struct SIMPLE t1, t2[20], *t3;
   ```

3. ```C
   //也可以用typedef创建新类型
   typedef struct
   {
       int a;
       char b;
       double c; 
   } Simple2;
   //现在可以用Simple2作为类型声明新的结构体变量
   Simple2 u1, u2[20], *u3;
   ```

##### 二、结构体声明（初始化）：

C#：

```C#
struct Books
{
   public string title;
   public string author;
   public string subject;
   public int book_id;
};  

Books Book1;        /* 声明 Book1，类型为 Books */
```

C:

```C
struct Books
{
   public string title;
   public string author;
   public string subject;
   public int book_id;
};  

struct Books Book1;        /* 声明 Book1，类型为 Books */
```

## C# 结构的特点

您已经用了一个简单的名为 Books 的结构。在 C# 中的结构与传统的 C 或 C++ 中的结构不同。C# 中的结构有以下特点：

- 结构可带有方法、字段、索引、属性、运算符方法和事件。
- 结构可定义构造函数，但不能定义析构函数。但是，您不能为结构定义无参构造函数。无参构造函数(默认)是自动定义的，且不能被改变。
- 与类不同，结构不能继承其他的结构或类。
- 结构不能作为其他结构或类的基础结构。
- 结构可实现一个或多个接口。
- 结构成员不能指定为 abstract、virtual 或 protected。
- 当您使用 **New** 操作符创建一个结构对象时，会调用适当的构造函数来创建结构。与类不同，结构可以不使用 New 操作符即可被实例化。
- 如果不使用 New 操作符，只有在所有的字段都被初始化之后，字段才被赋值，对象才被使用。

## 类 vs 结构

类和结构有以下几个基本的不同点：

- 类是引用类型，结构是值类型。
- 结构不支持继承。
- 结构不能声明默认的构造函数。

针对上述讨论，让我们重写前面的实例：

```C#
using System;
using System.Text;
     
struct Books
{
   private string title;
   private string author;
   private string subject;
   private int book_id;
   public void setValues(string t, string a, string s, int id)
   {
      title = t;
      author = a;
      subject = s;
      book_id =id;
   }
   public void display()
   {
      Console.WriteLine("Title : {0}", title);
      Console.WriteLine("Author : {0}", author);
      Console.WriteLine("Subject : {0}", subject);
      Console.WriteLine("Book_id :{0}", book_id);
   }

};  

public class testStructure
{
   public static void Main(string[] args)
   {

      Books Book1 = new Books(); /* 声明 Book1，类型为 Books */
      Books Book2 = new Books(); /* 声明 Book2，类型为 Books */

      /* book 1 详述 */
      Book1.setValues("C Programming",
      "Nuha Ali", "C Programming Tutorial",6495407);

      /* book 2 详述 */
      Book2.setValues("Telecom Billing",
      "Zara Ali", "Telecom Billing Tutorial", 6495700);

      /* 打印 Book1 信息 */
      Book1.display();

      /* 打印 Book2 信息 */
      Book2.display();

      Console.ReadKey();

   }
}
```

当上面的代码被编译和执行时，它会产生下列结果：

```C#
Title : C Programming
Author : Nuha Ali
Subject : C Programming Tutorial
Book_id : 6495407
Title : Telecom Billing
Author : Zara Ali
Subject : Telecom Billing Tutorial
Book_id : 6495700
```
