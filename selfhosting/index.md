---
layout: default-layout
title: Self-hosting License Tracking
keywords: self-hosting, activation, import
description: This page is about how to use self-hosting license tracking.
breadcrumbText: Self-hosting LTS
needAutoGenerateSidebar: true
---

# Self-hosting license tracking

> This article addresses Self-Hosting License Tracking. If you would rather let Dynamsoft track your license usage and not have to set up your own server for tracking, please see [Dynamsoft-hosting license tracking]({{site.dshosting}}index.html).

> If you have not purchased any Dynamsoft SDK license that requires usage tracking, please check out [how to purchase a license]({{site.about}}purchase.html).

The following assumes you have purchased a trackable license and have chosen "Self-Hosting" on the "Activate License" page in the [customer portal](https://www.dynamsoft.com/customer/license/fullLicense).

## Set Up LTS

To track the license yourself, you first need to install the License Tracking Server (LTS). Please read one of the following guides

* [Set up LTS on Windows]({{site.selfhosting}}ltsonwindows.html)
* [Set up LTS on Linux]({{site.selfhosting}}ltsonlinux.html)

After you have installed LTS on your server and got its UUID, you can proceed to the next step.

## Activate the License

On the "Activate License" page, there are a few steps for the activation.

* Set an Alias for your license

> This step is optional, you can just use the default Alias. Read more on [what is an Alias]({{site.about}}terms.html#alias).

* Input the `UUID` of the LTS hosted on your server, the UUID is found on the home page of your LTS.

![LTS-HomePage-001]({{site.assets}}imgs/lts-homepage.png)

> Read more on [what is a LTS UUID]({{site.about}}terms.html#lts-uuid)

* Click the "Activate" button.

Once the activation is done, an activated License File will be generated and downloaded automatically, the next step is to [import the license](#import-the-license).

> Read more on [what is a License File]({{site.about}}terms.html#license-file)

## Import the License

This step imports the License File into LTS so that you can configure and use the purchased license(s). Please see steps on [how to import the License File]({{site.selfhosting}}manageLTS.html#import-the-license-file).

## Configure the License

To configure the license is to manage the Handshake Code for the license. For more details, please see [how to manage the handshake code]({{site.common}}handshakeCodes.html).

> Read more on [what is a Handshake Code]({{site.about}}terms.html#handshake-code)

## Track the License

For Self-Hosting License Tracking, all usage data is submitted to the [ LTS ]({{site.about}}terms.html#license-tracking-server) hosted by yourself. You can

* [View activated license items]({{site.common}}licenseitems.html)
* [View the license usage statistics]({{site.common}}statistics.html)
* [Get notified about license status]({{site.common}}usagealerts.html)

> Read more on [the mechanism]({{site.common}}mechanism.html) behind license tracking.
