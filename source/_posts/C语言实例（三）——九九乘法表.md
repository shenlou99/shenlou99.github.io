---
title: C语言实例（三）——九九乘法表
date: 2023-01-29 09:51:23
tags: C
categories: C实例
---

```C
/*****
题目：输出9*9口诀。
******/

#include <stdio.h>
#include <stdlib.h>

int main()
{
    int i,j;
    for(i=1;i<10;i++)
    {
        for(j=1;j<10;j++)
        {
            if(j==9)
            {
                printf("%dx%d=%d\n",i,j,i*j);
            }
            else
            {
                printf("%dx%d=%d ",i,j,i*j);
            }
        }
    }
    return 0;
}

```

