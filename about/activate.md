---
layout: default-layout
title: How to activate a license
keywords: license, activation
description: This page describes how to activate a trackable license
breadcrumbText: Activate a License
needAutoGenerateSidebar: true
---

# How to activate a license

When you activate a purchased license, you will choose one of two activation options

* [Dynamsoft-Hosting]({{site.dshosting}}index.html).
* [Self-Hosting]({{site.selfhosting}}index.html)

![Choose-Activation-Option]({{site.assets}}imgs/activate-001.png)

> Once chosen and activated, this cannot be changed. So make sure you choose the correct one for your application.

Both options use the same software, Dynamsoft License Server ( DLS for short), to track the license usage. The differences are shown in the following table

> Read more on [what is a Dynamsoft License Server]({{site.about}}terms.html#dynamsoft-license-server)

|  | Dynamsoft-hosting| Self-hosting |
|:-:|:-:|:-:|
| Need to designate a server to host DLS | No | Yes |
| Need to install and manage DLS | No | Yes |
| Must have connection to Dynamsoft | Yes | No |
| Must send usage data to Dynamsoft | Yes | No |

Generally, you choose to host your own DLS if

* Your client devices may not be able to connect to the internet
* You don't want to share your usage data with Dynamsoft
* You believe your own server would work faster

If you decide to host your own DLS, please follow the instructions on [Self-hosting License Tracking]({{site.selfhosting}}index.html). Otherwise, read more on [Dynamsoft-hosting License Tracking]({{site.dshosting}}index.html).
