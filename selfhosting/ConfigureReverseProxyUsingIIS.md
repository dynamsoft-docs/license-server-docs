---
layout: default-layout
title: Install Dynamsoft Dynamsoft License Server on Windows
keywords: Install, Dynamsoft License Server, Windows
description: Steps and information about how to install Dynamsoft Dynamsoft License Server on Windows
breadcrumbText: Install DLS on Windows
needAutoGenerateSidebar: true
---

# Configure Reverse Proxy Using IIS

The following is an example on how to set up a reverse proxy using `IIS` for DLS for your reference. You can do the configuration yourself as long as you can achieve the requirement which is to redirect requests sent to "https://www.yoursite.com/dls/\*" to "https://127.0.0.1:48080/\*".

## Install IIS

Skip this step if you already have IIS installed.

## Install IIS URL Rewrite

Download and install IIS URL Rewrite from [here](https://www.iis.net/downloads/microsoft/url-rewrite).

## Configure URL Rewrite rules

![DLS-on-Windows-017]({{site.assets}}imgs/dlsonwin-017.png)

![DLS-on-Windows-018]({{site.assets}}imgs/dlsonwin-018.png)

![DLS-on-Windows-019]({{site.assets}}imgs/dlsonwin-019.png)

Let's configure the following rule for the server

``` text
Name：DLS-rewrite-rule
Pattern： ^dls/(.*)$
Rewrite URL：http://localhost:48080/{R:1}
```

![DLS-on-Windows-020]({{site.assets}}imgs/dlsonwin-020.png)


## Install Application Request Routing

Download and install Microsoft Application Request Routing [here](https://www.microsoft.com/en-us/download/confirmation.aspx?id=47333).

## Configure the proxy

![DLS-on-Windows-023]({{site.assets}}imgs/dlsonwin-023.png)

![DLS-on-Windows-024]({{site.assets}}imgs/dlsonwin-024.png)

![DLS-on-Windows-025]({{site.assets}}imgs/dlsonwin-025.png)

## Test that the configuration works

Open http://www.yoursite.com/dls/page/index.html and if you see the following page then the configuration is complete.

![DLS-on-Windows-026]({{site.assets}}imgs/dlsonwin-026.png)

## Configure SSL

Prepare a SSL certificate for your site (e.g. https://www.yoursite.com) and configure it properly. After that, you should be able to access the server by "https://www.yoursite.com/dls/page/index.html#/".

## Configure the Dynamsoft License Server

With the above steps, the Dynamsoft License Server will be listening on requests sent to this URL "https://www.yoursite.com/dls/". We recommend that you set up another Dynamsoft License Server on another machine as the standby Server(read more on [configure the DLS as the standby]({{site.selfhosting}}manageDLS.html#configure-a-standby-dls)). Assume the standby URL is "https://standby.yoursite.com/dls/", the following shows how to configure the server to be used (we take the JavaScript edition of Dynamsoft Barcode Reader as an example). Read more information [here]({{site.common}}mechanism.html#configure-dls).

``` javascript
Dynamsoft.DBR.BarcodeReader.licenseServer = ["https://www.yoursite.com/dls/", "https://standby.yoursite.com/dls/"];
```
