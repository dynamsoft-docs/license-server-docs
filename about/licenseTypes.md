---
layout: default-layout
title: About Dynamsoft Trackable Licenses
keywords: License Tracking, Trackable License
description: This page introduces the trackable licenses
breadcrumbText: Trackable Licenses
needAutoGenerateSidebar: true
---

# Trackable licenses

## Per Barcode Scan

This option is only for the Dynamsoft Barcode Reader SDK. It counts the number of barcodes successful found by the SDK. It is recommended if you can predict the number of barcode scans in a certain period of time in your application.

> For the JavaScript edition and the mobile edition, a barcode scan means a unique barcode value (of the same symbology) decoded from an image or a video frame. Some examples for your reference:
>
> | Examples	| Count of barcode scan |
> |:-:|:-:|
> | Two duplicated barcodes on an image | 1 |
> | Two different barcodes on an image | 2 |
> | Continuous scanning (video mode) of one barcode * | 1 |
> | Two barcodes with the same encoded text but different symbologies | 2 |
>
> *How to decide whether a barcode is a duplicate*
>  
> Each scanned barcode is buffered for 3 seconds during which time newly found barcodes will be compared with it. If a new barcode is exactly the same, that new barcode is not counted and is buffered for another 3 seconds while the old one is no longer buffered. If no match is found in that 3 seconds, the barcode is removed from the buffer.
>  
> For the mobile edition, 3 seconds is hardcoded. For the JavaScript edition, developers can specify the time with the API `duplicateForgetTime` which is 3 seconds by default.

## Per Device

Choose this option if you plan to scan a large number of barcodes with a limited number of devices. 

A device could mean different client in different deployment types.

| Deployment Type | Client Type |
|:-:|:-:|
| Browser | A specific browser |
| Mobile | A mobile device running iOS or Android |
| Server | Per 4 vCPUs on a Server machine |
| Desktop | Per 4 vCPUs on a desktop |
| Embedded | Per 4 vCPUs (if applicable) on an embedded device |

A client is identified by its [UUID]({{site.about}}terms.html#client-uuid).

Once a device gets authorized, it's considered active for 365 days, read more [here](#how-long-is-a-device-considered-active).

## Concurrent Device

This option is meant for the situation where you have a large number of client devices performing an unknown number of barcode scans sporadically.

One such device is defined the same way as with the [Per Device](#per-device) option. However, a concurrent device is a device that is configured to be active for only 3 minutes instead of 365 days, read more [here](#how-long-is-a-device-considered-active).

## Per Instance

This option is meant for the situation where multiple instances of the SDK are created to work on multiple tasks at the same time. It is based on the [Concurrent Device](#concurrent-device) license except that the limit is on the total number of active instances instead of the number of devices (UUIDs).

## Questions

### Can I filter unwanted barcodes to reduce the consumption of my license?

Yes. There are many pre-scanning settings you can apply to your barcode scanner.

For example, you can specify barcode format, limit the scanning to predefined regions or return only high-confidence values. For more settings, please refer to  [this page](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/decode-result.html).

### How long is a device considered active?

By default, a device is considered active as long as its UUID stays in the device list on the `LTS` . Once its UUID is removed, it is no longer considered "active". The following shows how LTS maintains the device list.

* Per Barcode Scan

Not applicable as no such list exists with this option.

* Per Device

The expiry date of the device is calculated like this

``` text
max ( min ( currentTime + 365 days, expiry date of the license ), currentTime + 7 days )
```

`currentTime` : the time that the device connects to the `LTS` either to get an authorization or to submit a usage report.

`LTS` reviews the list every 24 hours and removes all expired devices. Therefore, the longest time a device is regarded as active without actual usage is 372 days (example: authorized the same day the license is activated, re-authorized on the 365th day and get another 7 days, removed on the 372th day) and the shortest time is 7 days (example: authorized on the 365th day and removed on the 372th day).

* Concurrent Device

The expiry time of each active device is calculated like this

``` text
currentTime + (3 ~ 6 minutes)
```

`currentTime` : the time that the device connects to the `LTS` either to get an authorization or to perform a barcode scan.

The reason why the expiry time ranges from 3 to 6 minutes is to align it to the end of an absolute 3-minute slot. For example

If `currentTime` is 00:00:00, expiry time is 00:06:00; 
if `currentTime` is 00:01:25, expiry time is 00:06:00; 
if `currentTime` is 00:02:59, expiry time is 00:06:00; 
if `currentTime` is 00:03:00, expiry time is 00:09:00.

`LTS` checks the list every 1 minute and removes all expired devices. Therefore, the longest time a device is regarded as active without actual usage is 7 minutes (example: authorized at 00:00:00, expired at 00:06:00, removed at 00:07:00) and the shortest time is a bit more than 3 minutes (example: authorized at 00:02:59, expired at 00:06:00 and removed at 00:06:01).
