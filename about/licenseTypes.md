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

This option is meant for the [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/). It counts the number of barcodes successfully found by the SDK. It is recommended if you can predict the number of barcode scans in a certain period of time in your application.

> For the JavaScript edition and the Mobile edition, a barcode scan means a unique barcode value (of the same symbology) decoded from an image or a video frame. Some examples for your reference:
>
> | Examples	| Count of barcode scan |
> |:-:|:-:|
> | Two duplicated barcodes on an image | 1 |
> | Two different barcodes on an image | 2 |
> | Continuous scanning (video mode) of one barcode | 1 |
> | Two barcodes with the same encoded text but different symbologies | 2 |
>
> *How to decide whether a barcode is unique*
>  
> Each scanned barcode is buffered for 3 seconds during which time newly found barcodes will be compared with it. If a new barcode is exactly the same, that new barcode is not counted and it replaces the old one and gets buffered for another 3 seconds. If no match is found in that 3 seconds, the barcode is removed from the buffer.
>  
> For the Mobile edition, 3 seconds is hardcoded. For the JavaScript edition, developers can specify the time with the API `duplicateForgetTime` which is 3 seconds by default.

## Per Page

This option is recommended if you can predict the number of pages to be processed in a certain period of time in your application. It is used by:

* The [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/) and its extra modules (add-ons) such as the [Webcam Library](https://www.dynamsoft.com/web-twain/webcam-sdk-features/), the [PDF Rasterizer](https://www.dynamsoft.com/web-twain/pdf-to-image-javascript/) and the [OCR Engines](https://www.dynamsoft.com/web-twain/cpp-ocr-library/). The following shows how the counting is done.

| Module | How to count the pages |
|:-:|:-:|
| Core | The number of pages acquired from a scanner or imported from existing files. |
| Webcam | The number of frames captured. |
| PDFR | The number of pages rasterized from PDF files. |
| OCR | The number of pages processed by the OCR engine. |

> NOTE
>  
> * When Dynamic Web TWAIN is under a 'Per Page' license, the Barcode Reader can also be used as a module but its license will be of the type [Per Barcode Scan](#per-barcode-scan).
> * The [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) has a feature called [Intermediate Results](https://www.dynamsoft.com/barcode-reader/image-processing-intermediate-output/) and it also uses a 'Per Page' license where the number of images processed by this feature are counted.

## Per Device

Choose this option if you plan to perform a large number of operations like page scanning, barcode scanning or label recognition with a limited number of devices. 

Note that a device has different meanings for different [deployment types]({{site.about}}terms.html#deployment-type).

| Deployment Type | Client Type |
|:-:|:-:|
| Browser | A specific browser on a specific domain |
| Mobile | A mobile device running iOS or Android |
| Server (Workstation) | A computer running Windows or Linux which works as a server |
| Desktop | A computer running Windows, Linux or macOS (not working as a server) |
| Embedded | An ARM-based computer running Linux (not working as a server) |

> NOTE
>
> * For [Dynamic Web TWAIN](https://www.dynamsoft.com/web-twain/overview/), its trackable licenses only allow the "Browser" deployment type.
> * For "Browser" type, a specific domain means the same origin. Read more [here](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy).

A client is identified by its [UUID]({{site.about}}terms.html#client-uuid).

Once a device gets authorized, it's considered active for a limited time, read more [here](#how-long-is-a-device-considered-active).

## Concurrent Device

This option is meant for the situation where you have a large number of client devices performing an unknown number of operations like barcode scanning sporadically.

One such device is defined the same way as with the [Per Device](#per-device) option. However, a concurrent device is a device that is configured active for only a few minutes as opposed to the much longer duration for a [Per Device](#per-device) license, read more [here](#how-long-is-a-device-considered-active).

## Concurrent Instance

This option is meant for the situation where multiple instances of the SDK are created to work on multiple tasks at the same time. It is also based on the [Concurrent Device](#concurrent-device) license except that the limit is on the total number of active instances instead of the number of devices (UUIDs).

At present, this option is limited to the "Server" deployment type.

Read more on [How to use a Concurrent-Instance License](#how-to-use-a-concurrent-instance-license).

## Per Active Device

This option is meant for the situation where you have a large number of client devices, each of which is supposed to work continuously for a long time but not all the time.

One such device is maintained the same way as a concurrent device except that it is considered active for 24 hours instead of 3 minutes, read more [here](#how-long-is-a-device-considered-active).

This option is not available on Dynamsoft Web Store yet, [contact Dynamsoft Team](mailto:sales@dynamsoft.com) if you are interested.

## Per Domain

This option is meant for the situation where a very large number of devices will be performing an unknown number of opeations like barcode scanning and they all connect to a website on the same domain. The only limitation of this license type is the domain.

This option is not available on Dynamsoft Web Store, [contact Dynamsoft Team](mailto:sales@dynamsoft.com) if you are interested.

## Questions

### Can I filter unwanted barcodes to reduce the consumption of my license?

Yes. There are many pre-scanning settings you can apply to your barcode scanner.

For example, you can specify barcode format, limit the scanning to predefined regions or return only high-confidence values. For more settings, please refer to  [this page](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/decode-result.html).

### How long is a device considered active?

By default, a device is considered active as long as its UUID stays in the device list on the LTS. Once its UUID is removed, it is no longer considered "active". The following shows how LTS maintains the device list.

* Per Barcode Scan , Per Page

Not applicable as no such list exists with this option.

* Per Device

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