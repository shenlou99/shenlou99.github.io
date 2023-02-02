---
title: C语言实例（二）——字符串翻转
date: 2023-01-26 12:45:58
tags: C
categories: C实例
---

# C 语言实例 - 字符串翻转

### 一、使用递归来翻转字符串。

```C
#include <stdio.h>

void reverseSentence();
 
int main()
{
    printf("输入一个字符串: ");
    reverseSentence();
 
    return 0;
}
 
void reverseSentence()
{
    char c;
    scanf("%c", &c);
 
    if( c != '\n')
    {
        reverseSentence();
        printf("%c",c);
    }
}

```

输出结果为：

```C
输入一个字符串: runoob
boonur
```

### 二、普通方法

```C
#include <stdio.h>
#include <stdlib.h>
 
 
main()
{   
    char *str="i love you";
    char strrev1[10]; 
    int i,length;
    i=0;length=0;
    while(str[length]!='\0'){
    length++;
    }
    printf("字符串长度：%d",length); //可用<string.h>中的strlen代替 
    printf("原字符串：%s\n",str);
    while(length>=0){
     strrev1[i++]=str[--length];    
    }
    printf("反转后字符串：%s\n",strrev1);
    system("pause");
}
```

