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
  * System: 8 GB
  * Data: 20 GB
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

### Download the Dynamsoft License Server v2.3.5 installer, or just copy it over to a proper location

``` shell
cd /a-proper-location
wget https://tst.dynamsoft.com/public/download/dls/2.3.5/dynamsoft_dls-linux_x64-v2.3.5.tar.gz
```

### Unzip and start the Dynamsoft License Server

``` shell
# Unzip the installer
tar zxvf dynamsoft_dls-linux_x64-v2.3.5.tar.gz
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

Upon the first visit, you will be asked to set an admin password. A few things to note:

> 1. The default password is empty;
> 2. The user name is admin and it can not be changed;
> 3. **Currently, there isn’t a way to retrieve the password should it get lost. Therefore, please keep the password secure**.

After that, you will land on the home page where you can find the UUID of this DLS .

> This UUID is require when [activating your licenses]({{site.selfhosted}}index.html#activate-the-license).

![DLS-HomePage-001]({{site.assets}}imgs/dls-homepage.png)

If you see the above page, DLS is installed correctly and is ready to process requests. However, the requests can not reach it because it only listens on a local IP / Port. Therefore, the next step is to configure the network environment - reverse proxy - for it with the help of `nginx` .  See [Configure Reverse Proxy Using Nginx]({{site.selfhosted}}configurereverseproxyusingnginx.html) on how to redirect requests for `https://www.yoursite.com/dls/\*` to `https://127.0.0.1:48080/\*`.

> NOTE for Docker Users
>
> DLS requires persistent storage. Therefore, if `docker stop xxxxxx` was executed on the container, it needs to be restarted with `docker restart xxxxxx`.

## Configuration

With the above steps, DLS will be listening on requests sent to this URL `https://www.yoursite.com/dls/`. We recommend that you set up another DLS on another machine as the standby Server.

### Configure a Standby DLS

For maximum up time, a standby DLS is necessary. Assume you have installed two copies of DLS, the following are the steps to configure them

* Find the file `dls.json.sample` in the DLS directory, rename it to `dls.json`

* In the configuration, there are two settings: "serverMode" and "servers". We only need to change "servers". It accepts two values, the first specifies the main DLS URL and the second, the standby URL.

  * For the main DLS: `"servers": ["self", "https://standby.yoursite.com:port/"]`

  * For the standby DLS: `"servers": ["https://www.yoursite.com:port/", "self"]`

> NOTE that you need to configure both the main DLS and the standby DLS separately.

### Configure Server URLs

In order for the license client to know where to find DLS, the server URLs need to be embedded in the license string.

By default, when you first import a license and create a project, the license string for the project will already contain a server URL which is simply the host of the website. For example, if DLS is being visited like shown in the following image, then the license string will contain server URL as `https://192.168.8.221`.

![dls-url-001]({{site.assets}}imgs/dls-url-config-001.png)

In our case, this is incorrect and we need to change it to `https://192.168.8.221/dls`. We can click the button "Set Server URL" and change it:

![dls-url-002]({{site.assets}}imgs/dls-url-config-002.png)

Input the actual server URLs and save:

![dls-url-003]({{site.assets}}imgs/dls-url-config-003.png)

Once saved, all license strings will be updated to contain the server URLs.
