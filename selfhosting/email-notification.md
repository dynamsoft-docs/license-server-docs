---
layout: default-layout
title: Sample Folder Index Page
keywords: sample, index page
description: Sample folder index page
breadcrumbText: Sample Folder
---

# FAQs

## Can I add multiple recipants for the email notification?

Yes, simply use a semi colon to separate different emails.

## When do I receive the notifications?

The notifications are sent based on the usage and the license type.

The License Tracking Server checks the usage data every 10 minutes and if one of the following conditions is met, a notification email will be triggered.

### Per Barcode Scan, Per Page, Per Device

  
Quota usage exceeds 

* 75%
* 90%
* 95%
* 100%

### Concurrent Device

In the most recent 60 minutes, (the count of total authentication request failures) / (the count of total authentication requests) exceeds

* 10%
* 25%
* 50%
* 75%

> NOTE
>  
> If the quota overflow continues to be true yet not passing the next level (like 10% ~ 25%), no new email will be triggered. For example
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

## Can I adjust the conditions under which notifications are sent?

Currently, this is not supported.
