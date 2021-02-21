---
layout: default-layout
title: Configure HTTPS on Linux
keywords: Install, License Tracking Server, Linux, HTTPS
description: Steps and information about how to configure HTTPS on Linux
breadcrumbText: Configure HTTPS on Linux
needAutoGenerateSidebar: true
---

# Configure LTS on Linux

> If necessary, you can prepare a domain name for the License Tracking Server. For example, use "https://mainlts.yoursite.com" for the main server and "https://standbylts.yoursite.com" for the backup server.

To configure LTS on Linux, we first need a web server. We use `nginx` as an example.

## Install nginx

###	On CentOs

* Install

``` shell
rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm 
yum install nginx
```

![LTS-on-Linux-005]({{site.assets}}imgs/ltsonlinux-005.png)

* Start

``` shell
systemctl start nginx.server
```

* Configure the web server to start with the OS

``` shell
systemctl enable nginx.server 
```

### On Ubuntu

``` shell
sudo apt install nginx-full
sudo systemctl start nginx
sudo systemctl enable nginx
```

## Test nginx

Open http://localhost in a browser. If `nginx` was installed and started successfully, you should see a message like

``` text
······ Welcome to nginx! ······ 
```

## Configure nginx

### Open the configuration file

The file could either be `/etc/nginx/conf.d/default.conf` or `/etc/nginx/sites-enabled/default`.

### Add your server name

``` shell
server_name yoursite.com;
```

### Add reverse proxy

``` shell
location / {
  proxy_pass http://127.0.0.1:48080;
  proxy_set_header Host $proxy_host;
  proxy_set_header X-Real-IP $remote_addr;
  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}
```

### Restart the server

``` shell
sudo systemctl restart nginx
```

## Configure SSL

Use the following code to configure SSL. After that, HTTP requests to the port 80 will be redirected to the SSL port 443.

``` shell
yum -y install yum-utils 
yum-config-manager --enable rhui-REGION-rhel-server-extras rhui-REGION-rhel-server-optional 
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm 
yum -y install certbot python2-certbot-nginx 
certbot --nginx 
```

You may get an error like this

![LTS-on-Linux-009]({{site.assets}}imgs/ltsonlinux-009.png)

If you do, try running the following

``` shell
pip uninstall requests 
yum -y reinstall python-requests 
pip uninstall six 
yum -y reinstall python-six 
pip uninstall urllib3 
yum -y install python-urllib3 
```

If you get error about `urllib3` , reinstall it with

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

## Configure the License Tracking Server

With the above steps, you should be able to visit the License Tracking Server with the URL https://mainlts.yoursite.com/.

Now let's configure a main server and a standby server as well

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

Now the License Tracking Server is ready.
