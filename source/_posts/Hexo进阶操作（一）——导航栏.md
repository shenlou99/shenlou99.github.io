---
title: Hexo进阶操作（一）——导航栏
date: 2023-01-17 08:42:58
tags: hexo
categories: hexo
---

## 一、修改导航栏显示

在主题配置文件_config.yml中的menu：栏目添加自定义内容。

格式为：	显示名: 路径名（/默认为站点source文件夹） || fas fa-icon

免费图标网址：https://fontawesome.com.cn/faicons/

例子： 主页: / || fas fa-home	

## 二、导航栏匹配新页

实现点击导航栏显示新内容页：

Blog根目录鼠标右击，选择git bash here。输入以下命令：  

`hexo new page 导航栏名`

则会在站点source文件夹下创建一个以导航栏名为文件夹名字的文件夹。

该文件夹默认生成一个index.md文件，该文件front-master标识该导航栏新页的基本信息。

在index.md文件中，增加内容/操作，则可以在导航栏新页中显示内容/操作。

## 三、导航栏展开显示

menu:中修改配置，格式如下：

```
目录||fas fa-bars:
   归档: /archives/ || fas fa-archive
   标签: /tags/ || fas fa-tags
   分类: /categories/ || fas fa-folder-open
```

## 四、导航栏新页下载文件

在导航栏文件夹下放置本地文件，在该文件夹下index.md中输入如下markdown代码：

`[链接显示名](本地文件 "预览名")`

例子：

`[测试文件](test.pdf "这是pdf测试文件")`

