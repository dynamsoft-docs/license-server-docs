---
layout: default-layout
title: Install Dynamsoft License Tracking Server on Windows
keywords: Install, License Tracking Server, Windows
description: Steps and information about how to install Dynamsoft License Tracking Server on Windows
breadcrumbText: Install LTS on Windows
needAutoGenerateSidebar: true
---

# Install Dynamsoft License Tracking Server on Windows Server

## Example Environment

* CPU: Intel Core 2 Duo or AMD Athlon 64 X2 5600+
* Memory: 2G
* OS: Windows Server 2016
* Disk Space
  + System: 30 GB
  + Data: 20 GB

## Installation

### Run the installer

If you do not have the installer, please contact the [Dynamsoft Support team](mailto:support@dynamsoft.com).

### Test the server

Once the server is running, you can test it via the URL [http://localhost:48080/page/index.html](http://localhost:48080/page/index.html).

> If you changed the port during installation, you should use that port instead.

If you the following page shows up, then the server is installed correctly.

![LTS-on-Windows-001]({{site.assets}}imgs/ltsonwin-001.png)

## Install IIS

> This step assumes you have not installed IIS, if you have IIS already, you can skip this step.

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

Let's configure the following rule for the server

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

Open http://localhost/lts/page/index.html and if you see the following page then the configuration is complete.

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-026.png)

## Configure SSL

Prepare a SSL certificate for your site (e.g. https://www.yourdomain.com).

* Open Microsoft Management Console (run -> search -> mmc).

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-027.png)

* Add Snap-in for the root certificate

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-028.png)

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-029.png)

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-030.png)

* Import the certificate

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-031.png)

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-032.png)

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-033.png)

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-034.png)

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-035.png)

* Add the SSL port to your site

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-036.png)

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-037.png)

![LTS-on-Windows-026]({{site.assets}}imgs/ltsonwin-038.png)
