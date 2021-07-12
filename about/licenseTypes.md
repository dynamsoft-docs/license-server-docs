---
layout: default-layout
title: About Dynamsoft License Options
keywords: Licensing mode, licensing options
description: This page introduces all common licensing options
breadcrumbText: License Options
needAutoGenerateSidebar: true
---

# Dynamsoft License Options

## Per Barcode Scan
#### Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/)

With a Per Barcode Scan License, the SDK can be used to support a given number of unique barcode scans. For example, if the SDK is used to scan an image with four unique barcodes, it will be counted as four scans. When continuously scanning barcodes from a video stream, duplicated codes will be counted as one scan.

 Some examples for your reference:

 | Examples	| Count of barcode scan |
 |:-:|:-:|
 | Two duplicated barcodes on an image | 1 |
 | Two different barcodes on an image | 2 |
 | Continuous scanning (video mode) of one barcode | 1 |
 | Two barcodes with the same encoded text but different symbologies | 2 |

 By default, each scanned barcode is buffered for 3 seconds during which time newly found barcodes will be compared with it. If a new barcode is exactly the same, that new barcode is not counted and it replaces the old one and gets buffered for another 3 seconds. If no match is found in that 3 seconds, the barcode is removed from the buffer.
 For the JavaScript edition, developers can change the buffer time setting with the API `duplicateForgetTime`.

> NOTE
> 
> The Windows & Linux versions of Dynamsoft Barcode Reader SDK don't support the above duplicate-filtering logic, but please contact support@dynamosft.com for a workaround if you need to avoid per-scan license consumption by duplicate barcodes.

## Per Page
#### Applicable products: [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/)

With a Per Page License, the SDK can be used for processing a given number of document pages. For example, with a license for 100K pages of the scanner module of the SDK, you can scan up to 100K document pages and save them to your server.

| Module | How to count the pages |
|:-:|:-:|
| Core | The number of pages acquired from a scanner or imported from existing files. |
| Webcam | The number of frames captured. |
| PDFR | The number of pages rasterized from PDF files. |
| OCR | The number of pages processed by the OCR engine. |

> NOTE
>  
> * The 'Per Page' license option is also available for addons of the Dynamic Web TWAIN SDK, except for the Barcode Reader addon which uses [Per Barcode Scan](#per-barcode-scan).

## Per Client Device
#### Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) and [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/)

A client device can be any client-side hardware device (running a non-WebAssembly SDK) or any browser client (running a WebAssembly SDK). See blow table for more detail: 

| Deployment Type | Client Type |
|:-:|:-:|
| Browser | A specific browser on a specific [domain](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) |
| Mobile | A mobile device running iOS or Android |
| Desktop | A desktop computer running Windows, Linux or macOS |
| Embedded | An ARM-based computer running Linux |

A client is identified by its [UUID]({{site.about}}terms.html#client-uuid). Once a device gets authorized, it gets assigned a local license duration time. The local license duration time is decided by the specific type of device license you use. 

| Per-Device License Type | Local License Duration Time |
|:-:|:-:|
| Quarterly Active Device License | 90 days |
| Monthly Active Device License | 30 days |
| Daily Active Device License | 1 day (24 hours) |
| Concurrent Device License | 4 ~ 7 minutes |

The local license duration time would be expired if a device has not been used the SDK for the assigned length of validity time. Once expired, the license seat taken by the device would be automatically released from the license seat and thus can be reassigned to any active device. 

You can read more on [How long is a client-device considered active](#how-long-is-a-client-device-considered-active).

## Per Server
#### Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) (Windows/Linux edition) and [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/)

A Server is a device or computer that has the SDK loaded into its RAM. Server includes the following: 
(i) a networked device with the SDK installed that's accessible by multiple users who can independently operate the SDK from another machine, 
(ii) a networked device with the SDK running as a service that accepts connections from other machines or applications, 
(iii) a computer with the SDK running to service the public or multiple users, e.g. a kiosk or a scan station, and 
(iv) a web server with the SDK deployed that accepts end user connection to run the SDK on the client machines.

Please contact support@dynamsoft.com for more info about how to use a server license.


## Per Concurrent Instance
#### Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) (Windows/Linux edition)

The 'instance' here is the software instance for barcode reading created via APIs of the SDK. By creating N barcode reading instances, it means you can handle N barcode image reading requests simultaneously. 

At present, this option is limited to the "Server" deployment type.

Read more on [How to use a Concurrent-Instance License](#how-to-use-a-concurrent-instance-license).


## Per Domain
#### Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) (JavaScript edition) and [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/)

A Domain License allows unlimited usage of the SDK within one web application under a specific domain (e.g. *.dynamsoft.com). Subdomains like subdomainA.company.com and subdomainB.company.com are counted as one Domain.

For websites that use public domain names of multi-tenant cloud platforms (e.g. force.com), the domain license would be limited the unique subdomain such as dynamsoft.force.com.

If you are interested in this option, please [contact Dynamsoft Team](mailto:sales@dynamsoft.com).

## FAQs

### Can I filter unwanted barcodes to reduce the consumption of my license?

Yes. There are many pre-scanning settings you can apply to your barcode scanner.

For example, you can specify barcode format, limit the scanning to predefined regions or return only high-confidence values. For more settings, please refer to  [this page](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/decode-result.html).

### How long is a client device considered active?

By default, a device is considered active as long as its UUID stays in the device list on the LTS. Once its UUID is removed, it is no longer considered "active". The following shows how the license server maintains the device list.

* Per Device (Quarterly Active)

The expiry date of the device is calculated like this

``` text
max ( min ( currentTime + 90 days, expiry date of the license ), currentTime + 7 days )
```

`currentTime` : the time that the device connects to the LTS either to get an authorization or to submit a usage report.

LTS reviews the list every 24 hours and removes all expired devices. Therefore, the longest time a device is regarded as active without actual usage is 91 days and the shortest time is 7 days.


* Concurrent Device

The expiry time of each active device is calculated like this

``` text
currentTime + (4 ~ 7 minutes)
```

`currentTime` : the time that the device connects to the LTS either to get an authorization or to submit a usage report.

The reason why the expiry time ranges from 4 to 7 minutes is to align it to the end of an absolute 3-minute slot. For example

If `currentTime` is 00:00:00 ~ 00:01:59, expiry time is 00:06:00 and the valid time ranges from 4 to 6 minutes; if `currentTime` is 00:02:01 ~ 00:03:00, expiry time is 00:09:00 and the valid time ranges from 6 to 7 minutes. Expired devices are removed at the end of each 3-minute slot.

The reason for covering the next 3-minute slotis to avoid the license seat taken by another device while the previous device stays active and the reason why there is at least 4 minutes is to account for the time spent for requests from clients to reach LTS . 

### How to use a Concurrent-Instance License?

To use a concurrent-instance license, there are a few steps

1. Identify how many instances are needed on the device, then request the license seats from LTS; 

  > Note that these license seats are shared by all barcode-reading applications on the device

2. Check whether all license seats are taken with the API `GetIdleInstancesCount()` before creating a new instance;
3. Destroy an instance when it finishes its job to release the license seat.

The following shows a simple code snippet in C

```cpp
int main()
{
    char errorMsg[512];
    DM_LTSConnectionParameters connParameters;
    CBarcodeReader::InitLTSConnectionParameters(&connParameters);

    char handshakeCode[] = "Input your own handshake code.";
    connParameters.handshakeCode = handshakeCode;
    // Identify and request a certain number of license seats
    connParameters.maxConcurrentInstanceCount = 4;  
    int errorCode = CBarcodeReader::InitLicenseFromLTS(&connParameters, errorMsg, 512);
    if(errorCode != DBR_OK)
    {
        cout << errorMsg << endl;
        return -1;
    }

    // Check available license seats
    int count = CBarcodeReader::GetIdleInstancesCount();   
    if (count > 0)
    {
        // Create a new instance when there are seats left
        CBarcodeReader* reader = new CBarcodeReader();
        errorCode = reader.DecodeFile("Input image path");
        OutputResult(reader, errorCode);
        // Delete the instance after use
        delete reader;
    }
    else
    {
        // Request more seats from LTS or just wait for vacancies
        cout << "No license seat left!" << endl;
        return -1;
    }
    return 0;
}
```
