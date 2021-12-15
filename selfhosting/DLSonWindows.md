---
layout: default-layout
title: Install Dynamsoft Dynamsoft License Server on Windows
keywords: Install, Dynamsoft License Server, Windows
description: Steps and information about how to install Dynamsoft Dynamsoft License Server on Windows
breadcrumbText: Install DLS on Windows
needAutoGenerateSidebar: true
---

# Install Dynamsoft License Server on Windows Server

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

Upon the first visit, you will be asked to set an admin password. After that, you will land on the home page where you can find the UUID of this DLS .

> This UUID is require when [activating your licenses]({{site.selfhosting}}index.html#activate-the-license).

![DLS-HomePage-001]({{site.assets}}imgs/lts-homepage.png)

If the above page shows up, then the server is installed correctly and is ready to process requests. However, the requests may not be able to reach it because it only listens on a local IP / Port. Therefore, the next step is to configure the network environment - reverse proxy - for it with the help of `IIS` . Read more on [Configure Reverse Proxy Using IIS]({{site.selfhosting}}configurereverseproxyusingiis.html).
