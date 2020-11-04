---
layout: default-layout
title: Self-hosting License Tracking
keywords: self-hosting, activation, import
description: This page is about how to use self-hosting license tracking.
breadcrumbText: Self-hosting LTS
needAutoGenerateSidebar: true
---

# Self-hosting license tracking

> This article is about Self-Hosting License Tracking, if you would rather let Dynamsoft track your license usage, please see [Dynamsoft-hosting license tracking]({{site.dshosting}}index.html).

> If you have not purchased any Dynamsoft SDK license that requires usage tracking, please check out [how to purchase a license]({{site.about}}purchase.html).

The following assumes you have purchased a trackable license and have chosen "Self-Hosting" on the "Activate License" page in the [customer portal](https://www.dynamsoft.com/customer/license/fullLicense).

## Activate the License

On the "Activate License" page, there are a few steps for the activation.

* Set an Alias for your license

> This step is optional, you can just use the default Alias. Read more on [What is an Alias]({{site.about}}terms.html#alias).

* Input the `UUID` of the `LTS` hosted on your server

> This step is required, to get the `UUID` of your `LTS` , please see [How to set up LTS]({{site.selfhosting}}managelts.html#how-to-set-up-lts).

> Read more on [What is a LTS UUID]({{site.about}}terms.html#lts-uuid)

* Click the "Activate" button.

Once the activation is done, an activated License File will be generated and downloaded automatically, the next step is to [Import the license](#import-the-license).

> Read more on [What is a License File]({{site.about}}terms.html#license-file)

## Import the License

This step imports the License File into `LTS` so that you can configure and use the purchased license(s). Please see steps on [How to import the License File]({{site.selfhosting}}manageLTS.html#import-the-license-file).

## Configure the License

To configure the license is to manage the Handshake Code for the license. For more details, please see [how to manage the handshake code]({{site.common}}handshakeCodes.html).

> Read more on [What is a Handshake Code]({{site.about}}terms.html#handshake-code)

## Track the License

For Self-Hosting License Tracking, all usage data is submitted to the [ `LTS` ]({{site.about}}terms.html#license-tracking-service) hosted by yourself. You can

* [View activated license items]({{site.common}}licenseitems.html)
* [View the license usage statistics]({{site.common}}statistics.html)
* [Get notified about license status]({{site.common}}usagealerttriggers.html)
* [Add more quota to your license]({{site.about}}purchase.html#add-quota)

> Read more on [the mechanism]({{site.common}}mechanism.html) behind license tracking.
