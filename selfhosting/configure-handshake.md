---
layout: default-layout
title: Sample Folder Index Page
keywords: sample, index page
description: Sample folder index page
breadcrumbText: Sample Folder
---

You can configure a handshake code on the Handshake details page.

# FAQs

## How do I name a Handshake code?

The name of a handshake code consists of two parts

{Dynamsoft ID} - {custom string}

The first part must be your Dynamsoft ID. The second part can be any valid string. For example

* 216998-100025900
* 216998-vehicleCode

## What is a validation field and how to configure one?

A handshake code is just a string that shows up in your code. It is important to secure it so that other people who knows your handshake code can not use your license. The validation field is designed for this purpose.

A validation field is an unalterable characteristic of your application, at present, the following three are used

* Website Domain

> Usage: Dynamsoft Barcode Reader JavaScript Edition, Dynamic Web TWAIN

* Application ID

> Usage: Dynamsoft Barcode Reader Mobile Edition

* Process Name

> Usage: Dynamsoft Barcode Reader Server Edition & Embedded Edition

## How do I use Session Password?

The session password is another way to protect your license. Unlike the validation field which is essentially validating a characteristic of your application, the session password is a simpler and more flexible string that you set. To verify the password, all products use the same API, for example

* Dynamic Web TWAIN

``` javascript
Dynamsoft.WebTwainEnv.SessionPassword = "";
```

## Can I reuse a license item in different handshake codes?

Yes, a license can be used via different handshake codes, all usages from these codes will be counted against the license.

To add a license item, select it under **Add Items** to the left and add them to the right lane.
