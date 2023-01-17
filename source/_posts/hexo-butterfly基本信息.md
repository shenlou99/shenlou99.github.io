---
title: hexo+butterfly基本信息
date: 2023-01-17 09:11:56
tags: hexo,butterfly
categories: hexo,butterfly
---

## 一、Hexo站点信息

#### 1.public文件夹

存放网页基本配置等信息。

hexo clean 清除public文件夹。

hexo g 生成网站静态配置等信息。

#### 2.source文件夹

该文件夹作为主题配置文件中的根目录/。存放网页本地文件资源等。

#### 3.themes文件夹

该文件夹存放主题文件。

#### 4.node_modules

该文件夹一般不用备份，从github上clone到本地后，直接执行npm install命令就可以安装好所需插件

#### 5._config.yml

站点配置最重要的文件！！！站点配置信息更改全在此文件！！！

当执行 `hexo deploy` 时，Hexo 会将 `public` 目录中的文件和目录推送至 `_config.yml` 中指定的远端仓库和分支中，并且**完全覆盖**该分支下的已有内容

#### 6.gitignore

该文件规定哪些文件和文件夹不上传github

## 二、Butterfly主题信息

#### 1.languages文件夹

此文件夹记录英文对应中文翻译

#### 2.layout文件夹

此文件夹存放主题布局信息

#### 3.source文件夹

存放主题配置本地资源

#### 4._config.yml

主题配置最重要的文件！！！主题配置信息更改全在此文件！！！
