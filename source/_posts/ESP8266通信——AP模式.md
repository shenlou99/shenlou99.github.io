---
title: ESP8266通信——AP模式（电脑作为客户端，8266作为服务器，无需路由器）
date: 2023-03-09 16:32:41
tags: ESP8266
categories: WIFI通信
---

## 一、ESP8266配置

在串口助手中，通过AT指令配置ESP8266的AP模式。

```
1.AT									测试AT是否OK
2.AT+RST								软重启模组
3.AT+CWMODE=2							配置AP模式
4.AT+CWSAP_DEF="SSID","password",5,4   	设置ESP8266的AP信息
										AT+CWSAP_DEF=<ssid>,<pwd>,<chl>,<ecn>[,<max 										conn>][,<ssid hidden>]
5.AT+CIFSR								查询本机IP
6.AT+CIPMUX=1							开启多连接
7.AT+CIPSERVER=1,8080					开启服务器，端口号8080
8.AT+CIPSEND=0,5						AT+CIPSEND=clientid,length
9.AT+CIPSERVER=0 						关闭服务器

```

## 二、配置电脑客户端

在网络测试助手中，设置协议类型，TCP客户端，设置远程主机地址为ESP8266的IP地址，远程主机端口为ESP8266的端口，最后点击连接，等待连接成功。

## 三、数据收发

当建立连接后，双方即可正常收发数据。

电脑在网络测试助手发送即可。

ESP8266发送数据需要在串口助手中先发送AT指令：AT+CIPSEND=clientid,length，等待串口助手显示>后，再输入要具体发送的内容。
