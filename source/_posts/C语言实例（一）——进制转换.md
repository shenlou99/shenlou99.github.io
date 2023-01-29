---
title: C语言实例（一）——进制转换
date: 2023-01-26 11:23:12
tags: C
categories: C
---

## 一、二进制转换为十进制

```C
#include<stdio.h>
#include<math.h>

int ConvertBinaryToDecimal(long long n);
    
int main()
{
    long long n;
    printf("请输入一个二进制数：\n");
    scanf("%lld",&n);
    printf("二进制数%lld对应的十进制数为：%d",n,ConvertBinaryToDecimal(n));
    return 0;
}

int ConvertBinaryToDecimal(long long n)
{
    int remain;
    int i=0,decimalNumber=0;
    while(n!=0)
    {
        remain = n%10;
        n /= 10;
        decimalNumber += remain*pow(2,i);
        ++i;
    }
    return decimalNumber;
}
```

## 二、十进制转换为二进制

```C

#include <stdio.h>
#include <math.h>
 
long long convertDecimalToBinary(int n);
 
int main()
{
    int n;
    printf("输入一个十进制数: ");
    scanf("%d", &n);
    printf("十进制数 %d 转换为二进制位 %lld", n, convertDecimalToBinary(n));
    return 0;
}
 
long long convertDecimalToBinary(int n)
{
    long long binaryNumber = 0;
    int remainder, i = 1, step = 1;
 
    while (n!=0)
    {
        remainder = n%2;
        printf("Step %d: %d/2, 余数 = %d, 商 = %d\n", step++, n, remainder, n/2);
        n /= 2;
        binaryNumber += remainder*i;
        i *= 10;
    }
    return binaryNumber;
}
```

## 三、十进制转换为八进制

```C

#include <stdio.h>
#include <math.h>
 
int convertDecimalToOctal(int decimalNumber);
int main()
{
    int decimalNumber;
 
    printf("输入一个十进制数: ");
    scanf("%d", &decimalNumber);
 
    printf("十进制数 %d 转换为八进制为 %d", decimalNumber, convertDecimalToOctal(decimalNumber));
 
    return 0;
}
 
int convertDecimalToOctal(int decimalNumber)
{
    int octalNumber = 0, i = 1;
 
    while (decimalNumber != 0)
    {
        octalNumber += (decimalNumber % 8) * i;
        decimalNumber /= 8;
        i *= 10;
    }
 
    return octalNumber;
}
```

## 四、八进制转换为十进制

```C

#include <stdio.h>
#include <math.h>
 
long long convertOctalToDecimal(int octalNumber);
int main()
{
    int octalNumber;
 
    printf("输入一个八进制数: ");
    scanf("%d", &octalNumber);
 
    printf("八进制数 %d  转换为十进制为 %lld", octalNumber, convertOctalToDecimal(octalNumber));
 
    return 0;
}
 
long long convertOctalToDecimal(int octalNumber)
{
    int decimalNumber = 0, i = 0;
 
    while(octalNumber != 0)
    {
        decimalNumber += (octalNumber%10) * pow(8,i);
        ++i;
        octalNumber/=10;
    }
 
    i = 1;
 
    return decimalNumber;
}
```

