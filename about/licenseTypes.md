---
layout: default-layout
title: About Dynamsoft License Options
keywords: Licensing mode, licensing options
description: This page introduces all common licensing options
breadcrumbText: License Options
needAutoGenerateSidebar: true
noTitleIndex: true
---

# Dynamsoft License Options

The following shows the regular license options supported by Dynamsoft License Server (DLS).

- [Per Barcode Scan](#per-barcode-scan)
- [Per Page](#per-page)
- [Per Client Device](#per-client-device)
- [Per Concurrent Device](#per-concurrent-device)
- [Per Server](#per-server)
- [Per Domain](#per-domain)

> If these license options don't work for your application, you can contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) to learn about other available options.

## Per Barcode Scan

*Applicable product: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/)*

This license option limits the total number of unique & successful barcode scans that the SDK can perform.

To filter unneeded barcodes and reduce license consumption, you can configure your barcode scanning settings in a few ways. For example, you can specify the expected barcode formats, limit the scanning to predefined regions or return only high-confidence results. To learn more, see [How to filter and sort decoding results](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/decode-result.html).

NOTE: For the **Mobile** and **JavaScript** editions which usually scan consecutive image frames from a video input, there is a built-in deduplication logic which significantly lowers the number of scans, for example:

| Examples	| Count of barcode scans |
|:-:|:-:|
| 2 identical barcodes on the same image frame | 1 |
| 2 different barcodes on the same image frame | 2 |
| Multiple identical barcodes on consecutive image frames | 1 |

The deduplication is based on a preset interval which is 3 seconds by default. For the JavaScript edition, the interval can be set with the API [duplicateForgetTime](https://www.dynamsoft.com/barcode-reader/programming/javascript/api-reference/interface/ScanSettings.html?ver=latest).

## Per Page

*Applicable product: [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/)*

This license option limits the total number of document pages that the SDK can process. For example, with a license for 100K pages of the scanner module of the SDK, you can scan up to 100K document pages.

| Module | How pages are counted|
|:-:|:-:|
| Core | The number of pages acquired from a scanner or imported from existing files. |
| Webcam | The number of frames captured. |
| PDFR | The number of pages rasterized from PDF files. |
| OCR | The number of pages processed by the OCR engine. |

NOTE: The 'Per Page' license option also applies to the add-ons of the Dynamic Web TWAIN SDK, except for Barcode Reader which uses [Per Barcode Scan](#per-barcode-scan).

## Per Client Device

*Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/), [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/) and [Dynamsoft Label Recognizer SDK](https://www.dynamsoft.com/label-recognition/overview/)*

This license option limits the total number of active client devices.

For different applications, the definition of a client device is as follows:

| Aplication Type | Client Definition |
|:-:|:-:|
| Web | A specific browser from one origin (i.e., same protocol, port and hostname) <a href="https://developer.mozilla.org/en-US/docs/Glossary/Origin" target="_blank">Learn more about origin</a> |
| Mobile | A mobile device running iOS or Android |
| Desktop | A desktop computer running Windows, Linux or macOS |
| Embedded | An ARM-based computer running Linux |

Each client device is only active for a limited period of time, this is determined by the license type as shown in the following table:

| Per-Device License Type | Active time |
|:-:|:-:|
| Yearly Active Device License | min(currentTime + 365 days, expiry time of the license) |
| Quarterly Active Device License | min(currentTime + 90 days, expiry time of the license) |
| Monthly Active Device License | min(currentTime + 30 days, expiry time of the license) |
| Daily Active Device License | min(currentTime + 24 hours, expiry time of the license) |

> The active time starts from the first time the device is authorized. This behaviour can be changed so that the time starts from the first time the device uses the SDK. Contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) for more information.

When a device is active, its UUID is remembered by DLS and it takes a license seat. At the same time, the device stores a local license which makes sure the device can work online or offline as long as it is active. The active time is refreshed each time a device connects to DLS to reauthorize or submit a usage report. If the active device remains idle or offline for longer than its active time, it will stop working. At the same time, DLS will remove its UUID and release the license seat for another new device.

## Per Concurrent Device

*Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/), [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/) and [Dynamsoft Label Recognizer SDK](https://www.dynamsoft.com/label-recognition/overview/)*

This license option limits the maximum number of active client devices in a given 3-minute period.

> The definition of a client device in different application types is the same as [Per Client Device](#per-client-device)

For this license option, unlimited devices can be authorized and only after they have submitted usage reports will they be counted as active on DLS.

> During peak business hours, more devices may be active than usual and exceed the maximum allowed. To handle this, DLS allows mild but limited overuse of the license at no additional cost. Contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) for more information.

## Per Server

*Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) (Windows/Linux edition) and [Dynamsoft Label Recognizer SDK](https://www.dynamsoft.com/label-recognition/overview/) (Windows/Linux edition)*

This license option limits the total number of active servers.

An active server is a device or computer that has the SDK loaded into its RAM to perform operations like reading barcodes or recognizing text, etc.

Contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) for more information on how to use a per server license.

## Per Domain

*Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) (JavaScript edition) and [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/)*

This license option limits the domain name of a web application.

A per domain license allows unlimited usage of the SDK within one web application under a specific domain (e.g. `*.dynamsoft.com`). Multiple subdomains like `subdomainA.company.com` and `subdomainB.company.com` are counted as one domain.

For websites that use public domain names of multi-tenant cloud platforms (e.g. `force.com`), the domain license would be limited to a unique subdomain such as `dynamsoft.force.com`.

Contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) if you are interested in this license option.
