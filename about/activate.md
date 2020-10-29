---
layout: default-layout
title: Sample Page
keywords: sample, page
description: sample page
needAutoGenerateSidebar: true
---

# How to activate a license

You can choose one of the two activation options

> Once chosen, it can not be undone. So make sure you choose the correct one.

* Dynamsoft-Hosting
* Self-Hosting

Both options use the same software we call **License Tracking Service** ( `LTS` for short) to track the license usage. The differences are shown in the following table

> Read more on [what is a License Tracking Service]({{site.about}}terms.html#license-tracking-service)

| Question | Dynamsoft-hosting| Self-hosting |
|:-:|:-:|:-:|
| Need to designate a server to host `LTS` | No | Yes |
| Need to install and manage `LTS` | No | Yes |
| Must maintain connection to Dynamsoft | Yes | No |
| Must send usage data to Dynamsoft | Yes | No |

Generally, you choose to host your own `LTS` if

* Your client devices may not be able to connect to the internet
* You don't want to share your usage data with Dynamsoft
* You believe your own server would work faster

If you decide to host your own LTS, please read more on [Self-hosting License Tracking]({{site.selfhosting}}index.html). Otherwise, read more on [Dynamsoft-hosting License Tracking]({{site.dshosting}}index.html).
