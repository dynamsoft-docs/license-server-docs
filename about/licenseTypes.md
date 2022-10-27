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

- [Dynamsoft License Options](#dynamsoft-license-options)
  - [Per Barcode Scan](#per-barcode-scan)
  - [Per Page](#per-page)
  - [Per Client Device](#per-client-device)
  - [Per Concurrent Device](#per-concurrent-device)
  - [Per Server](#per-server)
  - [Per Domain](#per-domain)
  - [Per Instance](#per-instance)
    - [How the license restricts usage](#how-the-license-restricts-usage)
    - [How does the license handle multiple servers](#how-does-the-license-handle-multiple-servers)

> If these license options don't work for your application, you can contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) to learn about other available options.

## Per Barcode Scan

*Applicable product: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/)*

This license option limits the total number of unique & successful barcode scans that the SDK can perform.

To filter unneeded barcodes and reduce license consumption, you can configure your barcode scanning settings in a few ways. For example, you can specify the expected barcode formats, limit the scanning to predefined regions of the images or return only high-confidence results. To learn more, see [How to filter and sort decoding results](https://www.dynamsoft.com/barcode-reader/docs/core/programming/features/filter-and-sort.html?ver=latest).

NOTE: For the **Mobile** and **JavaScript** editions which usually scan consecutive image frames from a video input, there is a built-in deduplication logic which significantly lowers the number of scans, for example:

| Examples| Count of barcode scans |
|:-:|:-:|
| 2 identical barcodes on the same image frame | 1 |
| 2 different barcodes on the same image frame | 2 |
| Multiple identical barcodes on consecutive image frames | 1 |

The deduplication is based on a preset interval which is 3 seconds by default. For the JavaScript edition, the interval can be set with the API [duplicateForgetTime](https://www.dynamsoft.com/barcode-reader/docs/web/programming/javascript/api-reference/interface/ScanSettings.html).

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

The minimum time used for recording license usage is 3 minutes which is called a "time slice". Dynamsoft License Server devide each day into 480 such time slices.

This license option limits the maximum number of active client devices in a given time slice.

> The definition of a client device in different application types is the same as [Per Client Device](#per-client-device)

For this license option, unlimited devices can be authorized and only after they have submitted usage reports will they be counted as active on DLS.

> During peak business hours, more devices may be active than usual and exceed the maximum allowed. To handle this, DLS allows mild but limited overuse of the license at no additional cost. Contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) for more information.

## Per Server

*Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) (Windows/Linux edition), [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/) and [Dynamsoft Label Recognizer SDK](https://www.dynamsoft.com/label-recognition/overview/) (Windows/Linux edition)*

> For [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/), an offline "Per Server" license option is available but it uses a different licensing mechanism. Contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) for more information.

This license option limits the total number of active servers.

An active server is a device or computer that has the SDK loaded into its RAM to perform operations like reading barcodes or recognizing text, etc.

Contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) for more information on how to use a per server license.

## Per Domain

*Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) (JavaScript edition) and [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/)*

This license option limits the domain name of a web application.

A per domain license allows unlimited usage of the SDK within one web application under a specific domain (e.g. `*.dynamsoft.com`). Multiple subdomains like `subdomainA.company.com` and `subdomainB.company.com` are counted as one domain.

For websites that use public domain names of multi-tenant cloud platforms (e.g. `force.com`), the domain license would be limited to a unique subdomain such as `dynamsoft.force.com`.

Contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) if you are interested in this license option.

## Per Instance

*Applicable product: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) (Windows/Linux Server Edition)*

> At present, this option is limited to the "Server" [Deployment Type]({{site.about}}terms.html#deployment-type) only.

The minimum time used for recording license usage is 3 minutes which is called a "time slice". Dynamsoft License Server devide each day into 480 such time slices.

An instance refers to a barcode reader object running in a thread. This license option limits the maximum number of barcode reader instance in a given time slice.

Basic steps to use a per-instance license in your application:

- Step 1: identify how many instances might be needed on the device (server), then request the license seats from the license server;
  > Note that these license seats are shared by all barcode-reading applications on the device.
- Step 2: Check whether all license seats are taken with the API `GetIdleInstancesCount()` before creating a new instance;
  > In version 9.6.x (not yet released), Dynamsoft Barcode Reader will maintain an intermal thread pool so that you no longer need to monitor the idle seats anymore. Instead, you can initiate as many jobs as possible but expect different performance when the count of seats differs.
- Step 3: Destroy an instance when it finishes its job to release the license seat on the device.

### How the license restricts usage

Each per-instance license has a fixed quota N, when requesting license seats, you can ask for no more than N instances. These license seats are only considered "in use" when Dynamsoft Barcode Reader is used for barcode reading during a specific time slice. Such a time slice is called an active time slice.

### How does the license handle multiple servers

When running your application on a server farm or a scalable cloud service, each server machine makes its own license request. These individual license requests will all be granted which means all these servers can have their own independent license seats (up to N seats on each machine). This way, one server doesn't need to wait for other servers to release the license seats before getting its own.

Since multiple servers can get license seats at the same time, they can also run Dynamsoft Barcode Reader at the same time. Therefore, in a given time slice, more instances may be running than permitted by the licensing quota. Dynamsoft License Server handles this overusage through its built-in tolerance design, which allows 1000 x N additional active time slices for N instance licenses.

For example, let's say you purchased a license for 10 instances and ran your application on a server farm. During peak business hours, suppose there are 10 servers reading barcodes, each with 10 barcode reader instance seats. Then for each time slice, the recorded usage will be 100, with 90 considered extra and deducted from the total of 1000 x 10 = 10,000. When this carries on for a total of 112 time slices (5 hours 36 minutes), you will use up all the extra time slices (90 x 112 = 10080 > 10,000). When this happens, the Dynamsoft license server will flag the license as overused, and from that point on, only 10 license seats are allowed on all servers (if a server asks for 10 seats, the other servers cannot ask for any seats).

For more details on this licensing option, please [contact Dynamsoft Team](mailto:sales@dynamsoft.com).
