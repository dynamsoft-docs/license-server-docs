---
layout: default-layout
title: Dynamsoft License Activation
keywords: License Server, activation, license activation
description: Learn how to activate Dynamsoft 
breadcrumbText: Activation
needAutoGenerateSidebar: true
noTitleIndex: true
---

# How to Activate a License

When you activate a purchased license in the [customer portal](https://www.dynamsoft.com/customer/license/fullLicense), you must choose one of two activation options:

* Connect to Dynamsoft's License Server
* Connect to My Self-Hosted License Server

> Once activated, this cannot be changed, so make sure you choose the correct option for your license.

![Choose-Activation-Option]({{site.assets}}imgs/activate-001.png)

Both options use the same software, [Dynamsoft License Server (DLS)]({{site.about}}terms.html#dynamsoft-license-server), to manage the license. The differences are:

|                                        | Dynamsoft-hosted | Self-hosted |
| :------------------------------------: | :--------------: | :---------: |
| Need to designate a server to host DLS |        No        |     Yes     |
|     Need to install and manage DLS     |        No        |     Yes     |
|   Must have connection to Dynamsoft    |       Yes        |     No      |

Generally, you may choose to host your own DLS if:

* Your client devices may not be able to connect to the public internet.
* You do not want to share your usage data with Dynamsoft.
* A self-hosted DLS instance is more performant for your use case.

If you decide to host your own DLS, please follow the instructions on [Self-hosted DLS]({{site.selfhosted}}index.html). Otherwise, read the instructions below.

## Activate License

On the "Activate License" page, set an alias for your license or leave the default alias, then click the "Activate" button.

> [!TIP]
> Read more on [what is an alias]({{site.about}}terms.html#alias)

![Choose-Activation-Option]({{site.assets}}imgs/activate-001.png)

You will be prompted to confirm the request. Click "OK" to proceed.

![Proceed with activation]({{site.assets}}imgs/activate-002.png)

After activation, you will be redirected to the "License Details" page, where you can find the license key for the activated license.

![Check the license key]({{site.assets}}imgs/activate-003.png)

> [!TIP]
> Read more on [what is a license key]({{site.about}}terms.html#license-key)

## Manage License Keys

Managing a license key means configuring the project bound to this license key. For more details, see [Project Configuration]({{site.common}}project.html).

## Check License Usage

Dynamsoft products submit usage reports to DLS at runtime. The usage reports contain no information captured by the product - only numbers (for example, how many barcodes have been scanned or how many characters have been recognized). Based on these reports, DLS generates license usage reports.

* [View the license usage statistics]({{site.common}}statistics.html)
* [Get notified about license status]({{site.common}}usagealerts.html)
