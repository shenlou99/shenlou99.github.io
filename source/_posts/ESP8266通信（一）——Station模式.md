---
title: ESP8266通信——Station模式（8266客户端，电脑服务器，需要路由器中转）
date: 2023-03-09 16:13:35
tags: ESP8266
categories: WIFI通信
---

## 一、ESP8266配置

在串口助手中，通过AT指令配置ESP8266的station模式。

```
1.AT									测试AT是否OK
2.AT+RST								软重启模组
3.AT+CWMODE=1							配置station模式
4.AT+CWLAP								列出所有可连接热点
5.AT+CWJAP="SSID","password"			连接热点
6.AT+CIPMUX=1					ESP8266 作为服务器做多支持 5 个客户端的链接，id 分配顺序是 0-4
7.AT+CIFSR								查看ESP8266的IP
//当电脑端服务器配置完成后，执行下面AT指令
8.AT+CIPSTART="TCP","IP地址",端口号		 ESP8266作为客户端，连接电脑服务器端
9.AT+CIPSEND=0,5						AT+CIPSEND=clientid,length
10.AT+CIPCLOSE							关闭ESP8266与电脑的连接
11.AT+CIPQAP							关闭ESP8266与无线路由器的连接
```

## 二、配置电脑端服务器

在网络测试助手中，新建服务器，本地IP地址要确保与ESP8266的IP地址在同一网段，端口号设置8080，点击打开/启动。

然后在ESP8266中，执行上面第8条的AT指令，等待连接成功。

如果失败，ESP8266多重启几次试试。

## 三、数据收发

当建立连接后，双方即可正常通信，收发数据。

电脑在网络测试助手发送即可。

ESP8266发送数据需要在串口助手中先发送AT指令：AT+CIPSEND=clientid,length，等待串口助手显示>后，再输入要具体发送的内容。
