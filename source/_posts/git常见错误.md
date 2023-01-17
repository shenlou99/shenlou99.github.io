---
title: git常见错误
date: 2023-01-17 07:57:15
tags: git
categories: git
---

### 一、GitHub文件夹有白色箭头无法打开

1.删除文件夹里面的.git文件夹

2.执行git rm --cached 该文件夹路径

3.执行git add .

4.执行git commit -m ""

5.执行git push origin [branch_name]

### 二、完美解决 fatal: unable to access ‘https://github.com/…/.git’: Could not resolve host: github.com

	git config --global --unset http.proxy 
	git config --global --unset https.proxy

### 三、windows使用git时出现：warning: LF will be replaced by CRLF

```
1 $ rm -rf .git  // 删除.git
2 
3 $ git config --global core.autocrlf false  //禁用自动转换 
```
