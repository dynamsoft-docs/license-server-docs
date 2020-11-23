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

* CPU: 2C 
* Memory：2G
* Disk Space
  + System: 8G
  + Data: 20G
* OS：CentOs7.4

## Installation

Prepare a domain name for the License Tracking Server. For example, use "https://mainlts.yoursite.com" for the main server and "https://standbylts.yoursite.com" for the backup server. Make sure DNS is configured for these domain names.

### Initialize

``` shell
mkdir /data
mkfs -t ext4 /dev/nvme1n1
```

![LTS-on-Linux-001]({{site.assets}}imgs/ltsonlinux-001.png)

``` shell 
mount /dev/nvme1n1 /data
df -h

``` 

![LTS-on-Linux-002]({{site.assets}}imgs/ltsonlinux-002.png)

``` shell
vim /etc/fstab
/dev/nvme1n1 /data auto defaults 0 2
```

![LTS-on-Linux-003]({{site.assets}}imgs/ltsonlinux-003.png)

``` shell
mount -a
```

### Retrieve the LTS files

> If you already downloaded the file, you can just copy it over to the dir `/data`

``` shell
cd /data
wget http://********
```

### Unzip

``` shell
tar zxvf dynamsoft_lts-linux_x86_64-v2.0.1.tar.gz
```

### Set permissions

``` shell
chmod -R 777 /data/lts-linux
```

### Start License Tracking Server

``` shell
cd /data/lts-linux
sh startup.sh
```

### Check the Status to make sure the server is up

``` shell
ps -ef |grep dynamsoft
```

![LTS-on-Linux-004]({{site.assets}}imgs/ltsonlinux-004.png)

## Install nginx

###	Get the nginx web server

``` shell
[root@localhost ~]# rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm 
```

### Check the web server

``` shell
[root@localhost ~]# yum info nginx 
```

### Install the web server with yum

``` shell
[root@localhost ~]# yum install nginx
```

![LTS-on-Linux-005]({{site.assets}}imgs/ltsonlinux-005.png)

### Start the web server

``` shell
 [root@localhost ~]#systemctl start nginx.server
 ```

### Configure the web server to start with the OS

``` shell
systemctl enable nginx.server 
```

### Check the version of the web server

``` shell
[root@localhost ~]# nginx -v 
```

### Try accessing the web server

``` shell
[root@localhost ~]# curl -i localhost 
```

If successfuly, you should say a message like

``` text
······ Welcome to nginx! ······ 
```

## Configure nginx

### Open the configuration file and change `server_name`

``` shell
[root@localhost nginx]# vim /etc/nginx/conf.d/default.conf

server_name test.com;
```

### Reload the web server

``` shell
[root@localhost nginx]# /usr/sbin/nginx -s reload
```

<!--

### Add host to the hosts file

Use the `SwitchHosts` tool to add a host to the hosts file. For example

``` shell
192.168.10.11 test.com 
```

In your case, you should use a public IP instead of "192.168.10.11" that later your devices would use to connect to this Server and also use the correct domain instead of "test.com".

### Add exception in the firewall

Add an exception for inbound requests so that your devices can connect to the License Tracking Server correctly.
-->

### Add reverse proxy

![LTS-on-Linux-006]({{site.assets}}imgs/ltsonlinux-006.png)

### Verify the configuration file

![LTS-on-Linux-007]({{site.assets}}imgs/ltsonlinux-007.png)

### Reload the web server

![LTS-on-Linux-008]({{site.assets}}imgs/ltsonlinux-008.png)

### Configure SSL

Use the following code to configure SSL. After that, HTTP requests to the port 80 will be redirected to the SSL port 443.

``` shell
yum -y install yum-utils 
yum-config-manager --enable rhui-REGION-rhel-server-extras rhui-REGION-rhel-server-optional 
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm 
yum -y install certbot python2-certbot-nginx 
certbot --nginx 
```

You may get error like this

![LTS-on-Linux-009]({{site.assets}}imgs/ltsonlinux-009.png)

 
In this case, try

``` shell
pip uninstall requests 
yum -y reinstall python-requests 
pip uninstall six 
yum -y reinstall python-six 
pip uninstall urllib3 
yum -y install python-urllib3 
```

If you get error about `urllib3` , reinstall with

``` shell
pip install -I 'requests==2.6.0' urllib3 
```

After that, run the following again

``` shell
certbot --nginx 
```

![LTS-on-Linux-009]({{site.assets}}imgs/ltsonlinux-009.png)

### Configure auto-upgrade for the certificate

``` shell
echo "0 0, 12 * * * root python -c 'import random; import time; time.sleep(random.random() * 3600)' && certbot renew" | sudo tee -a /etc/crontab > /dev/null 
```

## Config License Trakcing Server

With the above steps, you should be able to visit the License Tracking Server with the URL https://mainlts.yoursite.com/.

Now we'll configure a main server and a standby server as well

### The main server

``` shell
vim /data/lts-linux/lts.json
{
  "serverMode": "main_standby", 
  "servers": ["self", "https://mainlts.yoursite.com"], 
}
```

### The standby server

``` shell
vim /data/lts-linux/lts.json
{
  "serverMode": "main_standby", 
  "servers": ["https://standbylts.yoursite.com", "self"], 
}
```
