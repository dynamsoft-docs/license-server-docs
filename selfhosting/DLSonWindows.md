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

Download the installer from [Dynamsoft-Licensing-Tracking-Server v2.2.19](https://tst.dynamsoft.com/public/download/dls/2.2.19/dynamsoft_dls-win_x64-v2.2.19.zip) and unzip it to a proper location. In our case, it's unzipped to **"E:\dynamsoft_dls-win_x64-v2.2.19"**.

There are two ways to get the server running:

#### Run DLS as an application 

This can be done simply by executing the batch file **"startup.bat"**

#### Run DLS as a service

This can be done with the help of the tool [NSSM](https://nssm.cc/). The following steps show how it works.

* Download [NSSM](https://nssm.cc/ci/nssm-2.24-101-g897c7ad.zip) and unzip, in our case, it's unzipped to **"E:\nssm-2.24"**
* Open cmd, navigate to the directory **"E:\nssm-2.24\win64"** and run the following command

```cmd
nssm install dynamsoft-dls
```

* A GUI will open, fill the parameters for the application like this (change the values according to where you put the files)

  + **Path**: `E:\dynamsoft_dls-win_x64-v2.2.19\win\bin\dynamsoftdlsx.exe`
  + **Startup directory**: `E:\dynamsoft_dls-win_x64-v2.2.19`
  + **Arguments**: `".\win\jre\bin\dynamsoftdls" --add-opens java.base/jdk.internal.loader=ALL-UNNAMED -jar ".\dls-2.2.19.jar" --server.port=48080 --data.port=50201`

![nssm-001]({{site.assets}}imgs/nssm-001.png)

* Switch to the last tab "Hooks" and choose "Application exit" as the Event and specify the parameter as 

  + **Command**: `E:\dynamsoft_dls-win_x64-v2.2.19\shutdown.bat`

![nssm-002]({{site.assets}}imgs/nssm-002.png)

* Press the button "Install Service" and you should be able to find dynamsoft-dls as one of the services in the services GUI or in **Task Manager -> Service**. If it is not started, start it.

### Test the server

Once the server is running, you can test it via the URL [http://127.0.0.1:48080/page/index.html](http://127.0.0.1:48080/page/index.html).

> If you changed the port during installation, you should use that port instead.

Upon the first visit, you will be asked to set an admin password. After that, you will land on the home page where you can find the UUID of this DLS .

> This UUID is require when [activating your licenses]({{site.selfhosting}}index.html#activate-the-license).

![DLS-HomePage-001]({{site.assets}}imgs/dls-homepage.png)

If the above page shows up, then the server is installed correctly and is ready to process requests. However, the requests may not be able to reach it because it only listens on a local IP / Port. Therefore, the next step is to configure the network environment - reverse proxy - for it with the help of `IIS` . Read more on [Configure Reverse Proxy Using IIS]({{site.selfhosting}}configurereverseproxyusingiis.html).
