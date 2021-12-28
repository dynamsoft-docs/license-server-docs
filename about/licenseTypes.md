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

## A Glance by Product

Dynamsoft Barcode Reader

- [Per Barcode Scan](#per-barcode-scan)
- [Per Client Device](#per-client-device)
- [Per Concurrent Device](#per-concurrent-device)
- [Per Concurrent Instance](#per-concurrent-instance)
- [Per Server](#per-server)
- [Per Domain](#per-domain)

Dynamic Web TWAIN

- [Per Page](#per-page)
- [Per Client Device](#per-client-device)
- [Per Concurrent Device](#per-concurrent-device)
- [Per Server](#per-server)
- [Per Domain](#per-domain)

## Per Barcode Scan

*Applicable product: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/)*

With a Per Barcode Scan License, the SDK can be used to support a given number of unique barcode scans. For example, if the SDK is used to scan an image with four barcodes, it will be counted as four scans. 

To filter unneeded barcodes and reduce license consumption, you can preset your barcode scanning settings in a few ways. For example, you can specify barcode format, limit the scanning to predefined regions or return only high-confidence values. Learn more: [How to filter and sort decoding results](https://www.dynamsoft.com/barcode-reader/parameters/scenario-settings/decode-result.html).

NOTE: For the **mobile** and **JavaScript** editions which usually scan consecutive image frames from a video input, there is a built-in deduplication logic which significantly lowers the number of scans, for example:

| Examples	| Count of barcode scans |
|:-:|:-:|
| 2 identical barcodes on the same image frame | 1 |
| 2 different barcodes on the same image frame | 2 |
| Multiple identical barcodes on consecutive image frames | 1 |

The deduplication is based on a preset interval which is 3 seconds by default. For the JavaScript edition, the interval can be set with the API [duplicateForgetTime](https://www.dynamsoft.com/barcode-reader/programming/javascript/api-reference/BarcodeScanner/interfaces.html#scansettings).

## Per Page

*Applicable product: [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/)*

With a Per Page License, the SDK can be used for processing a given number of document pages. For example, with a license for 100K pages of the scanner module of the SDK, you can scan up to 100K document pages.

| Module | How pages are counted|
|:-:|:-:|
| Core | The number of pages acquired from a scanner or imported from existing files. |
| Webcam | The number of frames captured. |
| PDFR | The number of pages rasterized from PDF files. |
| OCR | The number of pages processed by the OCR engine. |

NOTE: The 'Per Page' license option also applies to the add-ons of the Dynamic Web TWAIN SDK, except for Barcode Reader which uses [Per Barcode Scan](#per-barcode-scan).

## Per Client Device

*Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/), [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/) and [Dynamsoft Label Recognizer SDK](https://www.dynamsoft.com/label-recognition/overview/)*

A client device normally refers to the machine running a native application which has incorporated one of the Dynamsoft SDKs. 

For a **web application** that uses the javascript editions of Dynamsoft SDKs, a client device means a browser on the machine. The difference is based on the [Deployment Type]({{site.about}}terms.html#deployment-type) of the license as shown in the following table:

| Deployment Type | Client Type |
|:-:|:-:|
| Browser | A specific browser from one origin (i.e., same protocol, port and hostname) <a href="https://developer.mozilla.org/en-US/docs/Glossary/Origin" target="_blank">Learn more about origin</a> |
| Mobile | A mobile device running iOS or Android |
| Desktop | A desktop computer running Windows, Linux or macOS |
| Embedded | An ARM-based computer running Linux |

  A client is identified by its [UUID]({{site.about}}terms.html#client-uuid). Once a device gets authorized, it gets assigned a local license. The validity period of the local license is determined by the license type, as shown in the following table:

| Per-Device License Type | Local License Validity Period |
|:-:|:-:|
| Quarterly Active Device License | min(currentTime + 90 days, expiry time of the license) |
| Monthly Active Device License | min(currentTime + 30 days, expiry time of the license) |
| Daily Active Device License | min(currentTime + 24 hours, expiry time of the license) |

  The UUID of the device remains on the license server during the validity period of the local license and takes a license seat. After the validity period expires, the UUID on the license server will be deleted and the license seat becomes available again.

## Per Server

*Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) (Windows/Linux edition) and [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/)*

A Server is a device or computer that has the SDK loaded into its RAM. Server includes the following:

- a networked device with the SDK installed that's accessible by multiple users who can independently operate the SDK from another machine;
- a networked device with the SDK running as a service that accepts connections from other machines or applications;
- a computer with the SDK running to serve multiple users, e.g. a kiosk or a scan station;
- a web server with the SDK deployed that accepts end user connection to run the SDK on the client machines.

Please contact support@dynamsoft.com for more info about how to use a per-server license.

## Per Domain

*Applicable products: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) (JavaScript edition) and [Dynamic Web TWAIN SDK](https://www.dynamsoft.com/web-twain/overview/)*

A Domain License allows unlimited usage of the SDK within one web application under a specific domain (e.g. `\*.dynamsoft.com`). Multiple subdomains like `subdomainA.company.com` and `subdomainB.company.com` are counted as one Domain.

For websites that use public domain names of multi-tenant cloud platforms (e.g. `force.com`), the domain license would be limited the unique subdomain such as `dynamsoft.force.com`.

If you are interested in this option, please [contact Dynamsoft Team](mailto:sales@dynamsoft.com).

## Per Concurrent Device

*Applicable product: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/)*

With a N-concurrent-device license, N devices are allowed to read barcodes concurrently.

During peak business hours, more devices than usual might be reading barcodes and exceed the purchased quota. The license server allows mild overuse of the license at no additional cost. 

>The concurrency calculation is based on absolute 3-minute time slots. Each day is divided into 480 such time slots. When a device reports barcode scans to the license server, the server records an active device for the specific time slot during which the barcode scans were performed. For each time slot, there could be many active devices. When the number of active devices for a specific time slot exceeds the quota of the license (N), exceptions are recorded.

For more details on this licensing option, please [contact Dynamsoft Team](mailto:sales@dynamsoft.com).

## Per Concurrent Instance

*Applicable product: [Dynamsoft Barcode Reader SDK](https://www.dynamsoft.com/barcode-reader/overview/) (Windows/Linux Server Edition)*

An instance refers to a barcode reader object. With a N Concurrent Instance License, you can have up to N barcode reader objects working simultaneously.

> The concurrency calculation is similar to how it is done for [Per Concurrent Device](#per-concurrent-device) license. However, each device (server) can request X instances for it to use and the license server will record X instances active/used for the specific time slot no matter how many instances are actually in use on that machine. 

At present, this option is limited to the "Server" [Deployment Type]({{site.about}}terms.html#deployment-type).

Basic steps to use a concurrent-instance license in your application:

- Step 1: identify how many instances might be needed on the device (server), then request the license seats from the license server; 
  > Note that these license seats are shared by all barcode-reading applications on the device.
- Step 2: Check whether all license seats are taken with the API `GetIdleInstancesCount()` before creating a new instance; 
- Step 3: Destroy an instance when it finishes its job to release the license seat.

A sample code snippet in C:

```cpp
int main()
{
    char errorMsg[512];
    DM_DLSConnectionParameters connParameters;
    CBarcodeReader::InitDLSConnectionParameters(&connParameters);

    char handshakeCode[] = "Input your own handshake code.";
    connParameters.handshakeCode = handshakeCode;
    // Identify and request a certain number of license seats
    connParameters.maxConcurrentInstanceCount = 4;  
    int errorCode = CBarcodeReader::InitLicenseFromDLS(&connParameters, errorMsg, 512);
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
        // Request more seats from license server or wait for vacancies on the machine
        cout << "No license seat left!" << endl;
        return -1;
    }
    return 0;
}
```

For more details on this licensing option, please [contact Dynamsoft Team](mailto:sales@dynamsoft.com).
