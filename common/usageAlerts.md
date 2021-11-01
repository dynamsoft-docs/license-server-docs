---
layout: default-layout
title: About usage alerts
keywords: usage alert, notification
description: This page is about the email notifcation feature (usage alerts) of Dynamsoft Dynamsoft License Server
breadcrumbText: Usage Alerts
needAutoGenerateSidebar: true
---

# Usage Alerts

The Dynamsoft License Server checks the usage data every 10 minutes and if one of the following conditions is met, a notification email will be triggered and sent to you.

> NOTE
>  
> * The usage is based on a single License Item
> * If multiple conditions are met, the email will contain all the information. 

## Per Client Device

When the number of active devices (see FAQ below). reaches a certain percentage of the allowed total, you should be aware of this and take necessary measures, such as adding a new license. The preset percentages are:

* 75%
* 90%
* 95%
* 100%
* 110%

When the percentage reaches 100%, it means the license is exhausted. But considering that you may not be able to add a new license in time, the License Server allows another 10% of new devices to be authorized to use the software, so end users may not be immediately affected. When this happens, the customer should try to add a new license as soon as possible.

When the percentage reaches 110%, new devices will receive a license error when trying to use the software. Note that the devices that have been authorized before will continue to work.

## Per Barcode Scan or Per Page

When the number of barcodes you scan with Dynamsoft Barcode Reader or the number of pages you process with Dynamic Web TWAIN reaches a certain percentage of the allowed total, you should be aware of this and take necessary measures, such as adding a new license. The preset percentages are:

* 75%
* 90%
* 95%
* 100%
* 105%

When the percentage reaches 100%, it means the license is exhausted. But considering that you may not be able to add a new license in time, the License Server allows another 5% of barcode scans or pages, so end users may not be immediately affected. When this happens, the customer should try to add a new license as soon as possible.

When the percentage reaches 105%, all devices will receive a license error when trying to use the software.

## Per Concurrent Device or Per Concurrent Instance

With these types of licenses, the limit is on the total number of "concurrent devices or instances". Dynamsoft defines "concurrency" as being active (used the software) in the same period of 3 minutes. When more devices or instances are active for a specific 3-minute period, exceptions are recorded. When the number of total exceptions reaches a certain percentage of the allowed total, it means the concurrency limit (quota) is frequently exceeded and you should consider adding a license. The preset percentages are:

* 50%
* 75%
* 90%
* 100%

Note that even the first email triggered at the percentage of **50%** means the license is overused and you should take necessary measures as soon as possible. When **100%** is reached, the license will stop working and all devices will receive a license error.

## Questions

### How do you define 'Active Device'?

An active device is one that successfully acquired the authorization to use the software. Note that a device is considered "Active" only for a limited period of time after which it no longer takes a license seat. By default, the device is active for 90 days from the first authorization.

### Can I add multiple recipients for the email notification?

Yes. This is done differently for different hosting options.

For Self-hosting DLS, simply use a semicolon to separate different emails in the DLS management portal

![Configure recipients for notification on Self hosting]({{site.assets}}imgs/usagealerts-001.png)

For Dynamsoft-hosting DLS, email notifications are sent to all contacts configured for a specific order. You can check the contacts or add more in the customer portl

![Configure recipients for notification on DS hosting1]({{site.assets}}imgs/usagealerts-002.png)

![Configure recipients for notification on DS hosting2]({{site.assets}}imgs/usagealerts-003.png)

### When do I receive the notifications?

The notification emails are sent based on the usage and the license type as mentioned above.

### Can I adjust the conditions under which notifications are sent?

Currently, this is not supported.
