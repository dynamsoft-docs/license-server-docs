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

Download the installer from

[Dynamsoft-Licensing-Tracking-Server](https://tst.dynamsoft.com/public/download/lts/2.2/Dynamsoft-Licensing-Tracking-Server.exe)

### Test the server

Once the server is running, you can test it via the URL [http://127.0.0.1:48080/page/index.html](http://127.0.0.1:48080/page/index.html).

> If you changed the port during installation, you should use that port instead.

![LTS-on-Windows-001]({{site.assets}}imgs/ltsonwin-001.png)

If the above page shows up, then the server is installed correctly and is ready to process requests. However, the requests can not reach it because it only listens on a local IP / Port. Therefore, the next step is to configure the network environment - reverse proxy - for it with the help of `IIS`. Read more on [Configure Reverse Proxy Using IIS]({{site.selfhosting}}configurereverseproxyusingiis.html).