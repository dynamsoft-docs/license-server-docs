---
layout: default-layout
title: Install Dynamsoft License Tracking Server on Windows
keywords: Install, License Tracking Server, Windows
description: Steps and information about how to install Dynamsoft License Tracking Server on Windows
breadcrumbText: Install LTS on Windows
needAutoGenerateSidebar: true
---

# Configure Reverse Proxy Using IIS

The following is an example on how to set up a reverse proxy using `IIS` for `LTS` for your reference. You can do the configuration yourself as long as you can achieve the requirement which is to redirect requests sent to "https://www.yoursite.com/lts/\*" to "https://127.0.0.1:48080/\*".

## Install IIS

Skip this step if you already have IIS installed.

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

Let's configure the following rule for the server

``` text
Name：LTS-rewrite-rule
Pattern： ^lts/(.*)$
Rewrite URL：http://localhost:48080/{R:1}
```

![LTS-on-Windows-020]({{site.assets}}imgs/ltsonwin-020.png)

![LTS-on-Windows-021]({{site.assets}}imgs/ltsonwin-021.png)

![LTS-on-Windows-022]({{site.assets}}imgs/ltsonwin-022.png)

## Install Application Request Routing

Download Microsoft Application Request Routing [here](https://www.microsoft.com/en-us/download/confirmation.aspx?id=47333) and follow the screenshots below to get it installed.

![LTS-on-Windows-010]({{site.assets}}imgs/ltsonwin-010.png)

![LTS-on-Windows-011]({{site.assets}}imgs/ltsonwin-011.png)

![LTS-on-Windows-012]({{site.assets}}imgs/ltsonwin-012.png)

## Configure the proxy

![LTS-on-Windows-023]({{site.assets}}imgs/ltsonwin-023.png)

![LTS-on-Windows-024]({{site.assets}}imgs/ltsonwin-024.png)

![LTS-on-Windows-025]({{site.assets}}imgs/ltsonwin-025.png)

## Test that the configuration works

Open http://www.yoursite.com/lts/page/index.html and if you see the following page then the configuration is complete.

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-026.png)

## Configure SSL

Prepare a SSL certificate for your site (e.g. https://www.yoursite.com) and configure it properly. After that, you should be able to access the server by "https://www.yoursite.com/lts/page/index.html#/".

## Configure the License Tracking Server

With the above steps, the License Tracking Server will be listening on requests sent to this URL "https://www.yoursite.com/lts/". We recommend that you set up another License Tracking Server on another machine as the backup. Assume the backup URL is "https://backup.yoursite.com/lts/", the following shows how to configure the server to be used (we take the JavaScript edition of Dynamsoft Barcode Reader as an example). Read more information [here]({{site.common}}mechanism.html#configure-lts).

``` javascript
Dynamsoft.DBR.BarcodeReader.licenseServer = ["https://www.yoursite.com/lts/", "https://backup.yoursite.com/lts/"];
```
