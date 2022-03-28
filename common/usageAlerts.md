---
layout: default-layout
title: About usage alerts
keywords: usage alert, notification
description: This page is about the email notifcation feature (usage alerts) of Dynamsoft Dynamsoft License Server
breadcrumbText: Usage Alerts
needAutoGenerateSidebar: true
noTitleIndex: true
---

# Usage Alerts

Dynamsoft License Server checks the usage data every 10 minutes and if one of the following conditions is met, a notification email will be triggered and sent.

> NOTE
>  
> * If multiple conditions are met, there will only be one email containing all the information. 

## Per License Item

### Per Client Device

When the number of active devices reaches a certain percentage of the allowed total, you should be aware of this and take necessary measures such as adding a new license. The preset percentages are:

* 60%
* 80%
* 100%

> For Daily Active Device License, the email is only triggered at 100%.

When the percentage reaches 100%, it means the license is exhausted. Considering that you may not be able to add a new license in time, DLS allows another 10% of new devices to be authorized to use the software. When this happens, you should try to add a new license as soon as possible. When the percentage reaches 110%, new devices will receive a license error when trying to use the software. Note that the devices that have been authorized before will continue to work.

### Per Barcode Scan or Per Page

When the number of barcodes you scan with Dynamsoft Barcode Reader or the number of pages you process with Dynamic Web TWAIN reaches a certain percentage of the allowed total, you should be aware of this and take necessary measures, such as adding a new license. The preset percentages are:

* 60%
* 80%
* 100%

When the percentage reaches 100%, it means the license is exhausted. Considering that you may not be able to add a new license in time, DLS allows another 5% of barcode scans or pages. When this happens, you should try to add a new license as soon as possible. When the percentage reaches 105%, all devices will receive a license error when trying to use the software.

### Per Concurrent Device

For this license option, the notification is about overusage. DLS allows a limited amount of overusage per concurrent license item. When the overusage is consumed to a certain percentage, you should be aware of this and take necessary measures such as adding a new license. The preset percentages are:

* 60%
* 80%
* 100%

Note that even the first email triggered at the percentage of **60%** means the license is overused and you should take necessary measures as soon as possible.

## Per Project

When the number of failed authorization requests reaches the following percentages of all authorization requests, it means quite a few of your end users are not able to use your application. When you get the notification, you should either check the status of your license or get in touch with Dynamsoft as soon as possible.

* 10%
* 20%
* 40%
* 60%
* 80%
* 100%

## Questions

### Can I add multiple recipients for the email notification?

Yes. This is done differently for different hosting options.

When using Dynamsoft's DLS, email notifications are sent to all contacts configured for a specific order. You can check the contacts or add more in the customer portal

![Configure recipients for notification on DS hosting1]({{site.assets}}imgs/usagealerts-002.png)

![Configure recipients for notification on DS hosting2]({{site.assets}}imgs/usagealerts-003.png)

If you host your own DLS, simply use a semicolon to separate different emails in the DLS management portal

![Configure recipients for notification on Self hosting]({{site.assets}}imgs/usagealerts-001.png)

### When do I receive the notifications?

The notification emails are sent based on the usage and the license type as mentioned above.

### Can I adjust the conditions under which notifications are sent?

Currently, this is not supported.
