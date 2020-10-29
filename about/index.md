---
layout: default-layout
title: About Dynamsoft License Tracking Docs
keywords: License Tracking, index page
description: This page introduces the docs and the license types involved
breadcrumbText: About Dynamsoft License Tracking
---

# About the docs

These docs aim to help you learn and understand how Dynamsoft License Tracking works. Not all Dynamsoft Licenses are trackable, we say that a trackable license is one that isD compliant with [Dynamsoft License 2.0]({{site.about}}terms.html#license-2.0). The following are the current trackable licenses.

> The tracking is done on a per [handshake code]({{site.about}}terms.html#handshake-code) basis.

## Dynamsoft Barcode Reader

For the Dynamsoft Barcode Reader SDK, Dynamsoft offers the following trackable license options

### Per Barcode Scan

This option is simplest and recommended if you can predict the number of barcode scans in a certain period of time in your application.

A barcode scan means a unique barcode value (of the same symbology) decoded from an image or a video frame.

Some examples for your reference:

| Examples	| Count of barcode scan |
|:-:|:-:|
| Two duplicated barcodes on an image | 1 |
| Two different barcodes on an image | 2 |
| Continuous scanning (video mode) of one barcode * | 1 |
| Two barcodes with the same encoded text but different symbologies | 2 |

> * Scan Duplicates in Video Stream Mode:
>  
> Developers can specify a time frame ( `duplicateForgetTime` , default to 3 seconds) to filter out duplicates.
>
> A scan duplicate is when a barcode result reads the same value as a previously scanned barcode within `duplicateForgetTime` , say, 3 seconds. Once a scan is duplicated, the [time stamp] refreshes to the time when the latest duplicate was read

### Per Device

This option is recommended if you have a known number of devices and unknown number of barcode scans or that you need to scan a large number of barcodes on limited devices.

For each device, a random number is generated and mapped into a UUID-compatible string (also referred to as a UUID here), which is used to uniquely identify the device. In other words, we take the number of UUIDs as the number of devices.

Because of the way a UUID is generated and stored, a "device" refers to different things in different editions:

* JavaScript Edition: A UUID represents a specific browser on a certain domain.
* Mobile Edition, Embeded Edition: A UUID represents a device with the same CPU id, OS id and MAC address.
* Server Edition: A UUID represents a device with one or multiple fixed hardware (optional hardware includes CPU, Motherboard, MAC, Machine ID, etc.)

> NOTE:
>  
> * Multiple browsers on the same device are counted multiple devices.
> * The same browsers accessing multiple websites with different domains is counted separated per domain.
> * A UUID is cached in all cases, when the cached data is purged. The device will be regarded as a new one. In browsers, the UUID is cached in the indexedDB store for that specific website. In other cases, the UUID is cached in a hidden file.

### Concurrent Device

This option is meant for the situation where you have a large number of client devices but the barcode reading is done sporadically and you can not predict how many barcode scans will be performed.

One such device is defined the same way as in the [Per Device](#per-device) option. Essentially, a concurrent device is a device that is configured to be active for only 3 minutes (by default, it's 366 days). Also, LTS checks the UUIDs for concurrent devices and remove expired ones much faster (done every minute as opposed to the default 24 hours).

### Questions

#### How long is a device considered active?

By default, a device is considered active as long as its UUID stays in the usage database on the LTS. Once its UUID is removed, it is no longer active and considered "cleared".

All usage reports are submitted to LTS which examines the data and extracts the UUID, if such a UUID already exists in the database, its removal time is set to 366 days from "now". This means a device is active for at most 366 days.

LTS checks all UUIDs and removes those whose removal time has come. This is done every 24 hours.

#### Can I clear devices no longer using my application?

Yes, it is possible to clear devices which are still considered active but no longer using your application. However, this can only be done by contacting Dynamsoft Support Team. 

As mentioned in the answer to the previous question, a device is considered active for 366 days from its most recent usage of a Dynamsoft SDK. If you believe your client devices may alter in a shorter period, you can also request a special license that clears devices faster (say, 90 days).

#### What happens if my license quota is used up?

If the quota on your license is used up, all client devices will no longer be able to get an authentication token from the server and the SDK will throw a license error.
