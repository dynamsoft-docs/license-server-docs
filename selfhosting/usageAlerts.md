
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

### Per Barcode Scan/Per Device  

Notification emails are triggered when the ratio of consumed to total quota reaches the following targets: 

> The usage is based on a single License Item

* 75%
* 90%
* 95%
* 100%

### Concurrent Device

When the ratio of authentication request failures to the total number of requests reaches the following targets over the latest 60 minutes of app activity:

> The usage is based on single Handshake Code

* 10%
* 25%
* 50%
* 75%

> NOTE
>  
> If the condition continues to be true, yet the ratio is not passing the next level (let's take the jump from 10% to 25%), no new email will be triggered. For example
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

Yes, simply use a semicolon to separate different emails.

### When do I receive the notifications?

The notifications are sent based on the usage and the license type as mentioned above.

### Can I adjust the conditions under which notifications are sent?

Currently, this is not supported.
