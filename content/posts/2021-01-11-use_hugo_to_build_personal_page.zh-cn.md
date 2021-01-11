---
title:  如何使用RStudio+Hugo+Netlify搭建个人主页
author: Peng Wang
date: '2021-01-11'
slug: []
categories:
  - blog
tags: [hugo]
authors: [Peng Wang]
description: ''
externalLink: ''
series: []
---


- 本文尽量用最简单直接的语言搭配直接上手的代码来讲清楚如何搭建个人主页
- 必备软件：[R](https://cran.r-project.org/mirrors.html) (下载最新版本），[RStudio](https://rstudio.com/products/rstudio/download/#download)（下载最新版本的IDE）
- 必备网站：[Netlify](https://www.netlify.com) （用于将搭载好的网站承载在上面并进行发布）
- 可选网站：[GitHub](https://github.com) （用于和Netlify同步，方便经常更新个人网站的内容）

### 第一模块
1. 打开RStudio，输入下列代码
```R
install.packages("blogdown")   #安装blogdown包
blogdown::install_hugo(force=TRUE)  #安装hugo
```
2. 在RStudio的菜单栏里进行如下操作
  - File - New Project - New Directory - New Project
  - 在Directory Name中输入你想起的名字，例如“kw”
  - 在路径下拉菜单中选择你想把这个新的project放在哪里，建议选一个最容易找到的地方，例如就放在Downloads文件夹
  - 点击创建，RStudio会自动跳到你创建的新项目
3. 选择你喜欢的主题
  - [Hugo Themes](https://themes.gohugo.io)
  - 我们以[“aafu”](https://themes.gohugo.io/aafu/)为例 
  - 点击“download”，跳转到GitHub页面（不要慌，不需要你懂GitHub）
  - 记住主题的路径名，例如aafu，在GitHub上（用户名/库名）为“darshanbaral/aafu“
  - 一个劝告，小白不要选择太复杂的主题，例如那些有菜单，点击会有各种页面，甚至会有文章或者推文什么的
