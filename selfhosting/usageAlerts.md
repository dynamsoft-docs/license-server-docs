---
layout: default-layout
title: About usage alerts
keywords: usage alert, notification
description: This page is about the email notifcation feature (usage alerts) of Dynamsoft License Tracking Server
breadcrumbText: Usage Alerts
---

# Usage Alerts

The License Tracking Server checks the usage data every 10 minutes and if one of the following conditions is met, a notification email will be triggered.

## Dynamsoft Barcode Reader

### Per Barcode Scan, Per Device  

(Quota used) / (Total quota) exceeds 

> The usage is based on a single License Item

* 75%
* 90%
* 95%
* 100%

### Concurrent Device

In the most recent 60 minutes, (the count of total authentication request failures) / (the count of total authentication requests) exceeds

> The usage is based on single Handshake Code

* 10%
* 25%
* 50%
* 75%

> NOTE
>  
> If the condition continues to be true yet not passing the next level (like 10% ~ 25%), no new email will be triggered. For example
> * 12:40 Failure rate: 8%
> * 12:50 Failure rate:13%, first email triggered
> * 13:00 Failure rate:17%
> * 13:10 Failure rate:14%
> * 13:20 Failure rate:30%, second email triggered
> * 13:30 Failure rate:40%
> * 13:40 Failure rate:44%
> * 13:50 Failure rate:42%
> * 14:00 Failure rate:51%, third email triggered
> ...

## Questions

### Can I add multiple recipients for the email notification?

Yes. This is done differently for different hosting options.

For Self-hosting LTS, simply use a semicolon to separate different emails in the LTS management portal

![Configure recipients for notification on Self hosting]({{site.assets}}imgs/usagealerts-001.png})

For Dynamsoft-hosting LTS, email notifications are sent to all contacts configured for a specific order. You can check the contacts or add more in the customer portl

![Configure recipients for notification on DS hosting1]({{site.assets}}imgs/usagealerts-002.png})
![Configure recipients for notification on DS hosting2]({{site.assets}}imgs/usagealerts-003.png})

### When do I receive the notifications?

The notifications are sent based on the usage and the license type as mentioned above.

### Can I adjust the conditions under which notifications are sent?

Currently, this is not supported.
