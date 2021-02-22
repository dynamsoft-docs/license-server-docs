---
layout: default-layout
title: Install Dynamsoft License Tracking Server on Linux
keywords: Install, License Tracking Server, Linux
description: Steps and information about how to install Dynamsoft License Tracking Server on Linux
breadcrumbText: Install LTS on Linux
needAutoGenerateSidebar: true
---

# Install Dynamsoft License Tracking Server on Linux

## Example Environment

* CPU: 2 Core
* Memory：2 GB
* Disk Space
  + System: 8 GB
  + Data: 20 GB
* OS：CentOs7.4

## Installation

The following shows all the commands and steps required to set up the License Tracking Server

### Prepare a new disk to store LTS data (optional)

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

### Download the License Tracking Server installer (dynamsoft_lts-linux_x86_64-v2.0.1.tar.gz), or just copy it over to the dir `/data`

``` shell
cd /data
wget https://********
```

### Unzip and start the License Tracking Server

``` shell
# Unzip the installer
tar zxvf dynamsoft_lts-linux_x86_64-v2.0.1.tar.gz
# Set permissions
chmod -R 777 /data/lts-linux
# Start the server
cd /data/lts-linux
sh startup.sh
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

Now, if you visit [http://127.0.0.1:48080/page/index.html#/](http://127.0.0.1:48080/page/index.html#/) in the browser, you should be able to see the management portal of the License Tracking Server which indicates that it is ready to process requests. However, the requests can not reach it because it only listens on a local IP / Port. Therefore, the next step is to configure the network environment for it with the help of `nginx`. Read more on [Configure network for LTS on Linux]({{site.selfhosting}}configureltsonlinux.html#configure-lts-on-linux).