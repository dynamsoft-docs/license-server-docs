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

### Run DLS as a service

1. Download the installer from [Dynamsoft-Licensing-Tracking-Server v2.2.19](https://tst.dynamsoft.com/public/download/dls/2.2.19/dynamsoft_dls-win_x64-v2.2.19.zip) and unzip it to a proper location. In our case, it's unzipped to **"E:\dynamsoft_dls-win_x64-v2.2.19"**.

2. Install DLS as a service with the help of the tool `NSSM`. The following steps show how it works.

* Download [NSSM](https://nssm.cc/ci/nssm-2.24-101-g897c7ad.zip) and unzip, in our case, it's unzipped to **"E:\nssm-2.24"**
* Open cmd, navigate to the directory **"E:\nssm-2.24\win64"** and run the following command

```cmd
nssm install dynamsoft-dls
```

* A GUI will open, fill the parameters for the application like this (change the values according to where you put the files)

  * **Path**: `E:\dynamsoft_dls-win_x64-v2.2.19\win\bin\dynamsoftdlsx.exe`
  * **Startup directory**: `E:\dynamsoft_dls-win_x64-v2.2.19`
  * **Arguments**: `".\win\jre\bin\dynamsoftdls" --add-opens java.base/jdk.internal.loader=ALL-UNNAMED -jar ".\dls-2.2.19.jar" --server.port=48080 --data.port=50201`

![nssm-001]({{site.assets}}imgs/nssm-001.png)

* Switch to the last tab "Hooks" and choose "Application exit" as the Event and specify the parameter as

  * **Command**: `E:\dynamsoft_dls-win_x64-v2.2.19\shutdown.bat`

![nssm-002]({{site.assets}}imgs/nssm-002.png)

* Press the button "Install Service" and you should be able to find dynamsoft-dls as one of the services in the services GUI or in **Task Manager -> Service**. If it is not started, start it.

### Test the service

Once the server is running, you can test it via the URL [http://127.0.0.1:48080/page/index.html](http://127.0.0.1:48080/page/index.html).

> If you changed the port during installation, you should use that port instead.

Upon the first visit, you will be asked to set an admin password. After that, you will land on the home page where you can find the UUID of this DLS .

> This UUID is require when [activating your licenses]({{site.selfhosted}}index.html#activate-the-license).

![DLS-HomePage-001]({{site.assets}}imgs/dls-homepage.png)

If the above page shows up, then the server is installed correctly and is ready to process requests. However, the requests may not be able to reach it because it only listens on a local IP / Port. Therefore, the next step is to configure the network environment - reverse proxy - for it with the help of `IIS` . See [Configure Reverse Proxy Using IIS]({{site.selfhosted}}configurereverseproxyusingiis.html) on how to redirect requests sent to "https://www.yoursite.com/dls/\*" to "https://127.0.0.1:48080/\*".

## Configuration

With the above steps, DLS will be listening on requests sent to this URL "https://www.yoursite.com/dls/". We recommend that you set up another DLS on another machine as the standby Server.

### Configure a Standby DLS

For maximum up time, a standby DLS is necessary. Assume you have installed two copies of DLS, the following are the steps to configure them

* Find the file `dls.json.sample` in the DLS directory, rename it to `dls.json`

* In the configuration, there are two settings: "serverMode" and "servers". We only need to change "servers". It accepts two values, the first specifies the main DLS URL and the second, the standby URL.

  * For the main DLS: `"servers": ["self", "https://standby.yoursite.com/dls/"]`

  * For the standby DLS: `"servers": ["https://www.yoursite.com/dls/", "self"]`

> NOTE that you need to configure both the main DLS and the standby DLS separately.