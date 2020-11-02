---
layout: default-layout
title: Sample Folder Index Page
keywords: sample, index page
description: Sample folder index page
breadcrumbText: Sample Folder
---

# Minimum Server Configuration

* CPU: Intel Core 2 Duo or AMD Athlon 64 X2 5600+
* OS: Windows 7 / Windows 8 / Windows 10.
* VIDEO CARD: NVIDIA GeForce 7600 GT or ATI Radeon HD 2600 XT or Intel HD Graphics 3000 or better.
* FREE DISK SPACE: 30 GB.
* DEDICATED VIDEO RAM: 64 MB.

## Install LTS

* Run the installer 
* Configure ***
* Done

## Configure IIS components

ServerManager--Dashboard--Add
 

 

 

 

 

 

 

 

## Install  Application Request Routing 安装web访问代理模块

安装ARR（）
下载地址：https://www.microsoft.com/en-us/download/confirmation.aspx?id=47333
 

 

 
安装URL rewrite模块
下载地址：https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=urlrewrite2
 

 

 

 

##  Configure web proxy

 

 

 

## Configure URL Rewrite Rule

Name：LTS-rewrite-rule（可自定义）
Pattern： ^lts/(.*)$
Rewrite URL：http://localhost:48080/{R:1}
如下图所示
 

 

 
配置完后点击“Apply”应用配置。

## Configure Proxy

 

 

 
其他保持默认即可
访问LTS管理页面进行测试：
http://localhost/lts/Overview.html
 
