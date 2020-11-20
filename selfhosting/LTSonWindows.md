---
layout: default-layout
title: Install Dynamsoft License Tracking Service on Windows
keywords: Install, License Tracking Service, Windows
description: Steps and information about how to install Dynamsoft License Tracking Service on Windows
breadcrumbText: Install LTS on Windows
needAutoGenerateSidebar: true
---

# Install Dynamsoft License Tracking Service on Windows Server

## Environment

* CPU: Intel Core 2 Duo or AMD Athlon 64 X2 5600+
* Memory: 2G
* OS: Windows Server 2016
* Disk Space
  + System: 30G
  + Data: 20G

## Installation

### Run the installer

### Test the service

Once the service is running, you can test it via the URL [http://localhost:48080/page/index.html](http://localhost:48080/page/index.html).

> If you changed the port during installation, you should use that port instead.

If you see the following page showing up, then the service is installed correctly.

![LTS-on-Windows-001]({{site.assets}}imgs/ltsonwin-001.png)

## Install IIS

Go to ServerManager / Dashboard / Add and follow the screenshots below to add IIS web server.
 

![LTS-on-Windows-002]({{site.assets}}imgs/ltsonwin-002.png)

![LTS-on-Windows-003]({{site.assets}}imgs/ltsonwin-003.png)

![LTS-on-Windows-004]({{site.assets}}imgs/ltsonwin-004.png)

![LTS-on-Windows-005]({{site.assets}}imgs/ltsonwin-005.png)

![LTS-on-Windows-006]({{site.assets}}imgs/ltsonwin-006.png)

![LTS-on-Windows-007]({{site.assets}}imgs/ltsonwin-007.png)

![LTS-on-Windows-008]({{site.assets}}imgs/ltsonwin-008.png)

![LTS-on-Windows-009]({{site.assets}}imgs/ltsonwin-009.png)

## Install Application Request Routing

Download Microsoft Application Request Routing [here](https://www.microsoft.com/en-us/download/confirmation.aspx?id=47333) and follow the screenshots below to get it installed.

![LTS-on-Windows-010]({{site.assets}}imgs/ltsonwin-010.png)

![LTS-on-Windows-011]({{site.assets}}imgs/ltsonwin-011.png)

![LTS-on-Windows-012]({{site.assets}}imgs/ltsonwin-012.png)

## Install IIS URL Rewrite

Download IIS URL Rewrite [here](https://www.iis.net/downloads/microsoft/url-rewrite) and follow the screenshots below to get it installed.

![LTS-on-Windows-013]({{site.assets}}imgs/ltsonwin-013.png)

![LTS-on-Windows-014]({{site.assets}}imgs/ltsonwin-014.png)

![LTS-on-Windows-015]({{site.assets}}imgs/ltsonwin-015.png)

![LTS-on-Windows-016]({{site.assets}}imgs/ltsonwin-016.png)

## Configure URL Rewrite rules

![LTS-on-Windows-017]({{site.assets}}imgs/ltsonwin-017.png)

![LTS-on-Windows-018]({{site.assets}}imgs/ltsonwin-018.png)

![LTS-on-Windows-019]({{site.assets}}imgs/ltsonwin-019.png)

We'll configure this rule for the service

``` text
Name：LTS-rewrite-rule
Pattern： ^lts/(.*)$
Rewrite URL：http://localhost:48080/{R:1}
```

![LTS-on-Windows-020]({{site.assets}}imgs/ltsonwin-020.png)

![LTS-on-Windows-021]({{site.assets}}imgs/ltsonwin-021.png)

![LTS-on-Windows-022]({{site.assets}}imgs/ltsonwin-022.png)

## Configure the proxy

![LTS-on-Windows-023]({{site.assets}}imgs/ltsonwin-023.png)

![LTS-on-Windows-024]({{site.assets}}imgs/ltsonwin-024.png)

![LTS-on-Windows-025]({{site.assets}}imgs/ltsonwin-025.png)

## Test that the configuration works

Open http://localhost/lts/Overview.html and if you see the following page then the configuration is complete.

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-026.png)

 

 

 

 

 

 

 

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
 
