---
layout: default-layout
title: Install Dynamsoft Dynamsoft License Server on Linux
keywords: Install, Dynamsoft License Server, Linux
description: Steps and information about how to install Dynamsoft Dynamsoft License Server on Linux
breadcrumbText: Install DLS on Linux
needAutoGenerateSidebar: true
---

# Install Dynamsoft License Server on Linux

## Example Environment

* CPU: 2 Core
* Memory：2 GB
* Disk Space
  + System: 8 GB
  + Data: 20 GB
* OS：CentOs7.4

## Installation

The following shows all the commands and steps required to set up the Dynamsoft License Server

<!--### Prepare a new disk to store DLS data (optional)

``` shell
mkdir /data
# Specify a disk to mount, in our case, it is /dev/nvme1n1
mkfs -t ext4 /dev/nvme1n1
mount /dev/nvme1n1 /data
# Configure the mounting to be automatic
vim /etc/fstab
# Add the following line to the fstab file
/dev/nvme1n1 /data auto defaults 0 2
# Re-mount
mount -a
```
-->

### Download the Dynamsoft License Server v2.2.19 installer, or just copy it over to a proper location

``` shell
cd /a-proper-location
wget https://tst.dynamsoft.com/public/download/dls/2.2.19/dynamsoft_dls-linux_x64-v2.2.19.tar.gz
```

### Unzip and start the Dynamsoft License Server

``` shell
# Unzip the installer
tar zxvf dynamsoft_dls-linux_x64-v2.2.19.tar.gz
# Set permissions
chmod -R 777 ./dls-linux
# Start the server
cd ./dls-linux
./startup.sh
```

If you use Ubuntu, to start the server, try the following instead.

``` shell
# [optional] Install net-tools if it is not available (Ubuntu 20.04 may not come with it)
sudo apt install net-tools
./startup.sh
```

### Check the status to make sure the server is up

``` shell
ps -ef |grep dynamsoft
```

Now, if you visit [http://127.0.0.1:48080/page/index.html#/](http://127.0.0.1:48080/page/index.html#/) in the browser, you should be able to see the management portal of the Dynamsoft License Server. 

> You can edit startup.sh to change the listening ports.

Upon the first visit, you will be asked to set an admin password. After that, you will land on the home page where you can find the UUID of this DLS .

> This UUID is require when [activating your licenses]({{site.selfhosting}}index.html#activate-the-license).

![DLS-HomePage-001]({{site.assets}}imgs/dls-homepage.png)

If you see the above page, DLS is installed correctly and is ready to process requests. However, the requests can not reach it because it only listens on a local IP / Port. Therefore, the next step is to configure the network environment - reverse proxy - for it with the help of `nginx` . Read more on [Configure Reverse Proxy Using Nginx]({{site.selfhosting}}configurereverseproxyusingnginx.html).

### Docker Users Need to Know

Dynamsoft License Server requires persistent storage. Therefore, if `docker stop xxxxxx` was executed on the container, it needs to be restarted with `docker restart xxxxxx`.
