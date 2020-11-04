---
layout: default-layout
title: Manage License Tracking Service
keywords: License Tracking Service, management
description: This page is about how to manage License Tracking Service
breadcrumbText: Sample Folder
---

# Manage LTS

> Read more on [What is a LTS]({{site.about}}terms.html#license-tracking-service)

## How to set up LTS

### Download the latest LTS

At present, `LTS` is provided for either Windows or Linux. Download one that fits your environment.

* [For Windows Server](somelink)
* [For Linux Server](somelink)

### Install and configure LTS

Please read one of the following guides

* [On Windows]({{site.selfhosting}}ltsonwindows.html)
* [On Linux]({{site.selfhosting}}ltsonlinux.html)

### Log in LTS management portal

Once LTS is installed and configured, you can open its managment portal in the browser. The URL has the following pattern

``` text
https://{domain or IP of the server}:{port}/lts/page/#/index.html
```

The default credentials are 

``` text
UserName: admin
Password: 12345678
```

> If you are logging in for the first time, please don't forget to [change the password]({{site.selfhosting}}security.html#change-the-password)

Once logged in, you should be able to see the `UUID` of the `LTS` on the home page.

## Add license to LTS

### Download the License File

During [license activation]({{site.selfhosting}}index.html#activate-the-license), the License File should have already been downloaded. If you don't have the file yet, you can also download it from the [customer portal](https://officecn.dynamsoft.com:808/customer/license/fullLicense) by clicking the "Download License File (Activated)" button for that license.

> If the button reads "Download License File (Not Activated)", please first [activate the license]({{site.selfhosting}}index.html#activate-the-license).

### Import the License File

* Click "License Items" on the license menu to go to the "License Items" page
* Click "Select File" to open the License File you just downloaed and press "Import"

Once the importing is done

* You will see the license items contained in that License File in the *Activated License Items* table
* A Handshake Code is generated for that imported License File which includes all the license items and the next step is to [Configure the License](#configure-the-license)

> Read more on [About License Items]({{site.common}}licenseitems.html)

## Configure the License

To configure the license is to manage the Handshake Code for the license. For more details, please see [How to manage the handshake code]({{site.common}}handshakeCodes.html).

> Read more on [What is a Handshake Code]({{site.about}}terms.html#handshake-code)

## Configure usage alerts

When the quota on the license is about to be used up, you may want to be notified. `LTS` does it via email notifications. For more details, please see [How to manage usage alerts]({{site.common}}usagealerttriggers.html).

## Manage security

`LTS` manages your licenses, it's important to restrict access to the management portal. Therefore, make sure to [change the default password]({{site.selfhosting}}security.html#change-the-password) and keep the password secure.
