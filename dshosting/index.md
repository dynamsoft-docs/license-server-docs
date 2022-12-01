---
layout: default-layout
title: Dynamsoft-hosting license tracking
keywords: dynamsoft-hosting, license tracking
description: This page is about license tracking with Dynamsoft-Hosting Dynamsoft License Server
breadcrumbText: Dynamsoft-Hosting License Tracking
needAutoGenerateSidebar: true
---

# Connect to Dynamsoft-hosting License Server

> Dynamsoft has its license server deployed to the Amazon's AWS for customers to connect and consume their purchased license seats. As the license server is hosted on the cloud, the option only works if your to-be-licensed devices can connect to the internet. 
> If you must keep everything within your intranet, you can instead install the License Server program on your internal server machine. Please refer to [Self-hosting License Tracking]({{site.selfhosting}}index.html).

> To learn security features about the License Server, you can refer to [this page]({{site.about}}licensefaq.html).


## Activate the License

On the "Activate License" page, set an Alias for your license or leave the default Alias and click the "Activate" button.

![Choose-Activation-Option]({{site.assets}}imgs/activate-001.png)

> Read more on [what is an Alias]({{site.about}}terms.html#alias)


## Configure the License

To configure the license is to manage the Projects (used to be called Handshake Codes) for the license. For more details, please see [how to manage projects]({{site.common}}project.html).

> Read more on [what is a Project]({{site.about}}terms.html#project)

## Track the License

For Dynamsoft-Hosting License Tracking, all usage data is submitted to the [ DLS ]({{site.about}}terms.html#dynamsoft-license-server) hosted by Dynamsoft. You can

* [View activated license items]({{site.common}}licenseitems.html)
* [View the license usage statistics]({{site.common}}statistics.html)
* [Get notified about license status]({{site.common}}usagealerts.html)

> Read more about [the mechanism]({{site.common}}mechanism.html) behind license tracking.
