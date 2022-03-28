---
layout: default-layout
title: How to activate a license
keywords: license, activation
description: This page describes how to activate a trackable license
breadcrumbText: Activate a License
needAutoGenerateSidebar: true
noTitleIndex: true
---

# How to activate a license

When you activate a purchased license in the [customer portal](https://www.dynamsoft.com/customer/license/fullLicense), you need to choose one of two activation options

* Connect to Dynamsoft's License Server
* Connect to My Self-Hosted License Server

> Once activated, this cannot be changed. So make sure you choose the correct one for your license.

![Choose-Activation-Option]({{site.assets}}imgs/activate-001.png)

Both options use the same software, [Dynamsoft License Server (DLS)]({{site.about}}terms.html#dynamsoft-license-server), to manage the license. The differences are:

|  | Dynamsoft-hosted| Self-hosted |
|:-:|:-:|:-:|
| Need to designate a server to host DLS | No | Yes |
| Need to install and manage DLS | No | Yes |
| Must have connection to Dynamsoft | Yes | No |

Generally, you choose to host your own DLS if

* Your client devices may not be able to connect to the public internet
* You don't want to share your usage data with Dynamsoft
* You believe your own server would work faster

If you decide to host your own DLS, please follow the instructions on [Self-hosted DLS]({{site.selfhosted}}index.html). Otherwise, read the instructions below.

## Activate License

On the "Activate License" page, set an Alias for your license or leave the default Alias and click the "Activate" button.

> Read more on [what is Alias]({{site.about}}terms.html#alias)

![Choose-Activation-Option]({{site.assets}}imgs/activate-001.png)

You will be prompted to confirm the request, click "OK" to proceed.

![Proceed with activation]({{site.assets}}imgs/activate-002.png)

After the activation, you will be redirected to the "License Details" page where you can find the license key to use the activated license.

![Check the license key]({{site.assets}}imgs/activate-003.png)

> Read more on [what is license key]({{site.about}}terms.html#license-key)

## Manage License Keys

To manage a license key is to configure the project bound to this license key. For more details, please see [Project Configurartion]({{site.common}}project.html).

## Check License Usage

Dynamsoft products will submit usage reports to DLS at runtime. The usage reports contain no actual information captured by the product, but merely numbers like how many barcodes have been scanned or how many characters have been recognized, etc. With these reports, DLS generates reports about the usage of the licenses.

* [View the license usage statistics]({{site.common}}statistics.html)
* [Get notified about license status]({{site.common}}usagealerts.html)