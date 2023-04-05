---
layout: default-layout
title: Configure Reverse Proxy Using IIS
keywords: Install, Dynamsoft License Server, Windows
description: Steps and information about how to install Dynamsoft Dynamsoft License Server on Windows
breadcrumbText: Install DLS on Windows
needAutoGenerateSidebar: true
---

# Configure Reverse Proxy Using IIS

The following is an example on how to set up a reverse proxy using `IIS` for DLS for your reference. You can do the configuration yourself as long as you can achieve the requirement which is to redirect requests sent to `https://www.yoursite.com/dls/*` to `http://127.0.0.1:48080/*`.

## Install IIS

Skip this step if you already have IIS installed.

## Install IIS URL Rewrite

Download and install IIS URL Rewrite from [here](https://www.iis.net/downloads/microsoft/url-rewrite).

## Install Application Request Routing

Download and install Microsoft Application Request Routing [here](https://www.microsoft.com/en-us/download/confirmation.aspx?id=47333).

## Configure the proxy

![DLS-on-Windows-023]({{site.assets}}imgs/dlsonwin-023.png)

![DLS-on-Windows-024]({{site.assets}}imgs/dlsonwin-024.png)

![DLS-on-Windows-025]({{site.assets}}imgs/dlsonwin-025.png)

## Configure URL Rewrite rules

![DLS-on-Windows-017]({{site.assets}}imgs/dlsonwin-017.png)

![DLS-on-Windows-018]({{site.assets}}imgs/dlsonwin-018.png)

![DLS-on-Windows-019]({{site.assets}}imgs/dlsonwin-019.png)

Let's configure the following rule for the server

``` text
Name:DLS-rewrite-rule
Pattern: ^dls/(.*)$
Rewrite URL:http://localhost:48080/{R:1}
```

![DLS-on-Windows-020]({{site.assets}}imgs/dlsonwin-020.png)

## Test that the configuration works

Open `http://www.yoursite.com/dls/page/index.html` and if you see the following page then the configuration is complete.

![DLS-on-Windows-026]({{site.assets}}imgs/dlsonwin-026.png)

## Configure SSL

Prepare a SSL certificate for your site (e.g. `https://www.yoursite.com`) and configure it properly. After that, you should be able to access the server by `https://www.yoursite.com/dls/page/index.html#/`.

> If you use a JavaScript-based SDK, such as Dynamic Web TWAIN WebAssembly Edition or Dynamsoft Barcode Reader JavaScript Edition, you must configure the self-hosted DLS to run over a secure connection (HTTPS).
