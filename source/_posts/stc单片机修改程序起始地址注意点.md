---
title: stc单片机修改程序起始地址注意点
date: 2023-01-29 08:17:14
tags: stc
categories: 单片机
---

1.A51文件中更改AT值，即导致startup复位中断向量地址更改。
2.target的中断偏移向量更改，即导致单片机的中断偏移向量表更改。
3.更改target的EEPROM首地址，则导致单片机的用户程序地址更改。

所以，AT值和中断偏移值，不能和EEPROM首地址重合，否则会覆盖用户程序，导致用户程序无法运行。
