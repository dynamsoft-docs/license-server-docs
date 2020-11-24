---
layout: default-layout
title: About Dynamsoft Trackable Licenses
keywords: License Tracking, Trackable License
description: This page introduces the trackable licenses
breadcrumbText: Trackable Licenses
needAutoGenerateSidebar: true
---

# Trackable licenses

## Dynamsoft Barcode Reader

For the Dynamsoft Barcode Reader SDK, Dynamsoft offers the following trackable license options

### Per Barcode Scan

This option is simplest and recommended if you can predict the number of barcode scans in a certain period of time in your application.

For the JavaScript edition and the mobile edition, a barcode scan means a unique barcode value (of the same symbology) decoded from an image or a video frame.

Some examples for your reference:

| Examples	| Count of barcode scan |
|:-:|:-:|
| Two duplicated barcodes on an image | 1 |
| Two different barcodes on an image | 2 |
| Continuous scanning (video mode) of one barcode * | 1 |
| Two barcodes with the same encoded text but different symbologies | 2 |

> **How to decide whether a barcode is a duplicate**
> Each scanned barcode is buffered for 3 seconds during which time newly found barcodes will be compared with it. If a new barcode is exactly the same, that new barcode is not counted and is buffered for another 3 seconds while the old one is no longer buffered. If no match is found in that 3 seconds, the barcode is removed from the buffer. 
> For the mobile edition, 3 seconds is hardcoded. For the JavaScript edition, developers can specify the time with the API `duplicateForgetTime` which is 3 seconds by default.

#### Questions

##### Q: Can I filter unwanted barcodes to reduce the consumption of my license?

A: Yes. There are many pre-scanning settings you can apply to your barcode scanner.

For example, you can specify barcode format, limit the scanning to predefined regions or return only high-confidence values. For more settings, please refer to  [this page](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/decode-result.html).

### Per Device

This option is recommended if you have a known number of devices and unknown number of barcode scans or that you need to scan a large number of barcodes on limited devices. Dynamsoft supports two ways to generate a UUID, please see [Client UUID]({{site.about}}terms.html#client-uuid)

Once a device gets authorized, it's considered active for 365 days, read more [here](#how-long-is-a-device-considered-active).

### Concurrent Device

This option is meant for the situation where you have a large number of client devices but the barcode reading is done sporadically and you can not predict how many barcode scans will be performed.

One such device is defined the same way as in the [Per Device](#per-device) option. However, a concurrent device is a device that is configured to be active for only 3~7 minutes (for other editions, it's 365 days, read more [here](#how-long-is-a-device-considered-active)).

### Active Device

This option allows adjustment of the duration for determining whether the device is active. As shown above, with the [Per Device](#per-device) option, devices are considered active for up to 365 days while with [Concurrent Device](#per-device), it's considered active for 3~7 minutes. With "Active Device", the duration is set to 7 days by default and can be changed to a different time no shorter than 7 days.

The duration of the active status determines how many devices can actually use the software. Theoretically, the shorter the duration, the more devices can be used.

This option is not public, if you are interested, please contact [Dynamsoft Sales](mailto:sales@dynamsoft.com).

### Per Domain

This option is suitable for large organizations that have a large number of users using the SDK and cannot estimate the number of barcode scans. The only limitation for this kind of license is that all usage must be within the specified domain (e.g. `*.dynamsoft.com` ).

This option is not public, if you are interested, please contact [Dynamsoft Sales](mailto:sales@dynamsoft.com).

## Questions

### How long is a device considered active?

By default, a device is considered active as long as its UUID stays in the device list on the `LTS` . Once its UUID is removed, it is no longer active and considered "cleared".

#### How does LTS maintain the UUID list?

* Current Device

The expiry time of the device is calculated like this

``` text
currentTime + (3 ~ 6 minutes)
```

`currentTime` : the time that the device connects to the `LTS` either to get an authorization or to submit a usage report.

The reason why the expiry time ranges from 3 to 6 minutes is to align it to the end of an absolute 3-minute window. For example

If `currentTime` is 00:00:00, expiry time is 00:06:00; 
if `currentTime` is 00:01:25, expiry time is 00:06:00; 
if `currentTime` is 00:02:59, expiry time is 00:06:00; 
if `currentTime` is 00:03:00, expiry time is 00:09:00.

`LTS` checks the list on every 1 minute and removes all expired devices. Therefore, the longest time a device is regarded as active without actual usage is 7 minutes (example: authorized at 00:00:00, expired at 00:06:00, removed at 00:07:00) and the shortest time is a bit more than 3 minutes (example: authorized at 00:02:59, expired at 00:06:00 and removed at 00:06:01).

* Other license options except Active Device

The expiry date of the device is calculated like this

``` text
max ( min ( currentTime + 365 days, expiry date of the license ), currentTime + 7 days )
```

`currentTime` : the time that the device connects to the `LTS` either to get an authorization or to submit a usage report.

`LTS` reviews the list every 24 hours and removes all expired devices. Therefore, the longest time a device is regarded as active without actual usage is 372 days (example: authorized the same day the license is activated, re-authorized on the 365th day and get another 7 days, removed on the 372th day) and the shortest time is 7 days (example: authorized on the 365th day and removed on the 372th day).

* Active Device

The difference with the above one is that instead of 365 days, the duration can be an adjustable 7 or more days. Contact [Dynamsoft Sales](mailto:sales@dynamsoft.com) for more information.

### Can I clear devices no longer using my application?

Yes, it is possible to clear devices which are still considered active but no longer using your application. However, this may come with a cost and can only be done by contacting [Dynamsoft Support Team](mailto:support@dynamsoft.com).

### What happens if my license quota is used up?

| License Type | Behavior |
|:-:|:-:|
| Per Barcode Scan | All clients fail with a license error |
| Per Device | No new device can get authorized |
| Concurrent Device | New devices will fail to get authorized until old devices become inactive |
| Active Device | Same as Per Device |
| Per Domain | Not applicable |
