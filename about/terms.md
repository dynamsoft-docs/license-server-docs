---
layout: default-layout
title: Terms involved in Dynamsoft License Tracking
keywords: Terms, Dynamsoft, License Tracking, 
description: This page has defintions and descriptions about Dynamsoft License Tracking Terms
breadcrumbText: Terms
needAutoGenerateSidebar: true
---

# Terms

## License 2.0

License 2.0 is the next-generation licensing protocol designed and implemented by Dynamsoft for our products, including Dynamsoft Barcode Reader, Dynamic Web TWAIN, and more.

The following table shows the differences between License 1.0 and 2.0

| | License 1.0 | License 2.0 |
|:-:|:-:|:-:|
| Expirable | Yes | Yes |
| Usage Trackable | No | Yes |
| Hardware binding | Required | Optional |
| Use Handshake Code | No | Yes |
| Use the license itself | Yes | No |

## Public Trial License

A public trial license is a special license provided by Dynamsoft for all users to test Dynamsoft Products for up to 7 days.

This license is based on License 2.0, therefore, network is required for it to work.

Dynamsoft is gradually rolling out this license in the products. If you are having trouble getting this license to work, please feel free to [contact us](https://www.dynamsoft.com/company/contact/).

## Private Trial License

The old trial license was a string of alphanumeric characters and was not trackable. A private trial license is designed to replace it.

Simply put, a private trial license is a [Per Device]({{site.about}}licensetypes.html#per-device) license good for 30 days and 30 devices and should only be used for product evaluation purposes.

## Alias

An Alias is another way to identify a license. You can set a meaningful Alias to a license so that you can easily identify the purpose of the license.

A default Alias is created automatically that follows the pattern `DM_{License Id}_Date{Activation Date}` .  A more meaningful Alias could be something like `BarcodeReader_License_For_Dynamsoft_ABC_Project` .

A few things to know about the Alias

* It can only be changed when the license is new. Once the license is activated, it can no longer be changed.
* The Alias will show up in the [License File](#license-file) as a field. 
* A License File has just one Alias.

## License Item

A License Item contains a permit to use a product (for example, a license item can be described as a "10, 000-Barcode-Scan package for using Dynamsoft Barcode Reader within Browsers". The license item cannot be split. 

## Organization ID

An Organization ID uniquely specifies an organization which represents the licensee of one or multiple License Item(s).

## Handshake Code

The permits in License Items are not consumed directly by applications because 

* The same permit can be used by multiple applications
* The same application can use multiple permits from different License Items

Therefore, Dynamsoft invented the concept of a "Handshake Code". An application using a Dynamsoft SDK gets authorized by Dynamsoft's [License Tracking Server](#license-tracking-server) through a specific Handshake Code within the License Tracking Server.

* The same Handshake Code can be configured to contain permits from different License Items
* The permit from a single License Item can be shared by multiple Handshake Codes

By doing this, the code of your application doesn't need to change, even if different permits are needed at a later date.

A few things to note

* Quota consumption is counted against the License Item in use
* Statistics are also summarized per Handshake Code

## Default Handshake Code

For each new organization added to a [ LTS ](#license-tracking-server), a default Handshake Code is created. This Handshake Code is used by default when an application only specifies the license by its [Organization ID](#organization-id).

## Validation Field

A Handshake Code is a string that is set in your code and it is important to secure it so that it cannot be used by any other parties. For that, the Handshake Code comes with a security setting called `Validation Field` .

A Validation Field is a static characteristic of your application, meaning that once set, it cannot be changed. At present, the following three Validation Fields are supported

* Website Domain

> Applicable Products: Dynamsoft Barcode Reader via "Browser Deployment", Dynamic Web TWAIN

* Application ID

> Applicable Products: Dynamsoft Barcode Reader via "Mobile Deployment"

* Process Name

> Applicable Products: Dynamsoft Barcode Reader for desktop and server deployments; Dynamsoft Barcode Reader Embedded Edition

## Session Password

The Session Password is another way to protect your license. Unlike the Validation Field, which is essentially validating a characteristic of your application, the Session Password is a simpler and more flexible string that you set in your application. To verify the password, all products have a similar API, let's take the Barcode Reader for example:

### Dynamsoft Barcode Reader

* JavaScript

``` javascript
Dynamsoft.DBR.BarcodeReader.handshakeCode = "DynamsoftID-CustomCode";
Dynamsoft.DBR.BarcodeReader.sessionPassword = "The-Password-You-Set";
let reader = await Dynamsoft.DBR.BarcodeReader.createInstance();
```

* C++

``` cpp
int iRet = -1;
char szErrorMsg[256];
DM_LTSConnectionParameters ltspar;    
CBarcodeReader::InitLTSConnectionParameters(&ltspar);
ltspar.handshakeCode = "Your-HandshakeCode"; // Please replace the handshakeCode with your own
ltspar.SessionPassword = "The-Password-You-Set";
iRet = CBarcodeReader::InitLicenseFromLTS(&ltspar, szErrorMsg, 256);
if (iRet != DBR_OK)
{
    printf("Error code: %d. Error message: %s\n", iRet, szErrorMsg);
    return -1;
}
```

* CSharp

``` csharp
DMLTSConnectionParameters ltspar = BarcodeReader.InitLTSConnectionParamters();           
ltspar.HandshakeCode = "Your-HandshakeCode";
ltspar.SessionPassword = "The-Password-You-Set";
EnumErrorCode iRet = BarcodeReader.InitLicenseFromLTS(ltspar, out strErrorMSG);
```

* Java

``` java
DMLTSConnectionParameters ltspar = BarcodeReader.initLTSConnectionParameters();
ltspar.handshakeCode = "Your-HandshakeCode";
ltspar.sessionPassword = "The-Password-You-Set";
BarcodeReader.initLicenseFromLTS(ltspar);
```

* Java for Android

``` java
DBRLTSLicenseVerificationListener ltsListener = new DBRLTSLicenseVerificationListener() { 
    @Override  
    public void LTSLicenseVerificationCallback(boolean success, Exception error) { 
        if (error != null){ Log.i("lts error: ", error.getMessage());  } 
    } 
};
```

* Objective-C for iOS

``` c
@interface <DMLTSLicenseVerificationDelegate>

iDMLTSConnectionParameters* lts = [[iDMLTSConnectionParameters alloc] init];
lts.handshakeCode = @"Your-HandshakeCode";
lts.sessionPassword = @"The-Password-You-Set";
_dbr = [[DynamsoftBarcodeReader alloc] initLicenseFromLTS:lts verificationDelegate:self];

* (void)LTSLicenseVerificationCallback:(bool)isSuccess error:(NSError * _Nullable)error

{
    NSNumber* boolNumber = [NSNumber numberWithBool:isSuccess];
    dispatch_async(dispatch_get_main_queue(), ^{
        [self->m_verificationReceiver performSelector:self->m_verificationCallback withObject:boolNumber withObject:error];
        NSLog(@"ifsuccess : %@",boolNumber);
        NSLog(@"error code: %ld:",(long)error.code);
        NSLog(@"errormsg : %@",error.userInfo);
    });
}
```

<!--

* Dynamic Web TWAIN

``` javascript
Dynamsoft.WebTwainEnv.SessionPassword = "";
```

-->

## License File

A License File describes one or multiple [License Items](#license-item) and the status of these items.

Each License File has a unique `LicenseId` and an [ `Alias` ](#alias). You can also find out the version of the license scheme, whether the license has been activated, etc. For example

``` text
LicenseId: 100028117
Alias: 
LicenseTextVersion: 2.0
CustomerDynamId: 216998
LicenseStatus: Activated
LicenseItems:
...//one or multiple License Items
```

When you place an order, a License File containing all the License Items will automatically be generated. Before the License is activated, you will see the "LicenseStatus" as "new" in the file. Otherwise it will say "Activated".

If you are using the Dynamsoft-hosting License Tracking Server, the License Files are only information about your orders for your reference and are not required for the license to operate. However, if you are hosting the License Tracking Server yourself, you need the License File in order to add the License Items to that LTS for license tracking.

## Deployment Type

The deployment type means how and where the software is being used. For example. The type "mobile" means the software runs in native mobile applications on iOS and Android while the type "browser" means the software runs in web applications within browsers on any operating system. At present, the types are

| Deployment Type | Application Type |
|:-:|:-:|
| Browser | A web application running in browsers |
| Mobile | A native application running on iOS or Android |
| Server (Workstation) | An application running on Windows or Linux that processes requests from other client devices |
| Desktop | An application running on Windows, Linux or macOS that handles requests on this specific device. |
| Embedded | An application running on ARM-based Linux that handles requests on this specific device. |

## License Tracking Server

The License Tracking Server, or LTS for short, is a proprietary software developed by Dynamsoft to track license usage.

Dynamsoft hosts a copy of the software for customers who don't want to track the usage themselves. For customers who would rather track the license usage themselves, the software can also be self-hosted. For more information, please see:

* [Self-hosting License Tracking]({{site.selfhosting}}index.html)
* [Dynamsoft-hosting License Tracking]({{site.dshosting}}index.html)

## Tolerance Stage

Dynamsoft allows excessive usage of the licenses in case the licensee fails to extend or expand the license in time. For difference license types, this stage means different things:

| License Type | Tolerance Stage |
|:-:|:-:|
| `Per Barcode Scan` | `round(5% * quota)` is allowed after the actual quota runs out. |
| `Per Page` | `round(5% * quota)` is allowed after the actual quota runs out. |
| `Per Device` | `round(10% * quota)` is allowed after the actual quota runs out. |
| `Concurrent Device` | A number of exceptions are allowed and the number grows as time passes. |
| `Concurrent Instance` | A number of exceptions are allowed and the number grows as time passes. |
| `Active Device` | A number of exceptions are allowed and the number grows as time passes. |
| All Types | 7 days are allowed after the license expires. |

## LTS UUID

The UUID here means a unique ID for the machine where LTS is deployed. This UUID will be bound to the license during license activation. After that, this license can only be imported and used on this particular machine. Therefore, make sure this machine assigned for production usage is stable.

You can find the UUID of your LTS on the [admin portal](https://www.dynamsoft.com/license-tracking/docs/selfhosting/managelts.html?ver=latest#log-in-lts-management-portal) once you have successfully installed LTS .

A UUID is bound to one or multiple unique hardware identification labels which include

* ProcessorId
* Media Access Control Address
* Machine ID
* Motherboard Serial Number

If the hardware changes and any of the bound labels is different, the license binding will fail and the license will be unusable. Therefore, be cautious when changing server hardware.

## Client UUID

Each client machine (a device) is also identified by its UUID. This UUID is generated the first time the client machine gets authorized to use a license. All usage reports generated on this client will include this UUID too.

The following table shows the differences between LTS UUID and Client UUID

| | LTS UUID | Client UUID |
|:-:|:-:|:-:|
| Bound to the License | Yes | No |
| Bound to usage reports | No | Yes |
| Hardware binding | Required | Optional |

For each device, a UUID is generated which is used to uniquely identify the device. In other words, we take the number of UUIDs as the total number of devices supported by the license.

### Generate a UUID

* JavaScript Edition: A random number is generated and mapped into a UUID-compatible string. This UUID is cached in the browser's indexedDB. A UUID represents a specific browser on a certain domain.

> NOTE:
>  
> * Multiple browsers on the same device are counted as multiple devices since there will be a UUID generated for each browser.
> * The same browsers accessing multiple websites with different domains is counted separately per domain.

* Mobile Edition, Embedded Edition: A UUID represents a device with the same CPU id, OS id and MAC address.

* Server Edition: A UUID represents a device with one or multiple fixed hardware (optional hardware includes CPU, Motherboard, MAC, Machine ID, etc.)

### Soft Binding

For editions other than the JavaScript edition, the UUID is generated by default via "Soft Binding" which means the gathered device information is combined with a random number to generate the UUID. This random number is only cached on the device and not sent anywhere. This means two things:

* With the UUID alone, it is impossible to know the actual device information thus ensures privacy
* If the cached random number is accidentally lost, the UUID will fail to identify this device and it'll be regarded as a new device

If you don't mind sharing the device information with the LTS , you can also generate UUID via "Hard Binding".

### Hard Binding

"Hard Binding" means a UUID is directly generated with the collected device information (only for Desktop/Server/Mobile/Embeded editions).

* Desktop/Server/Embeded: the CPU ID and OS ID are collected
* Mobile: the unique device string provided by the device itself is collected

The good news is that as long as you don't change the CPU or reinstall the operating system, a device will always be recognized by the LTS . On the other hand, this means that the LTS can decrypt the UUID to obtain the actual device information.

### Questions

#### Q: Does the UUID give away information about my device?

A: By default, the answer is no because [Soft Binding](#soft-binding) is used. But if you choose to use [Hard Binding](#hand-binding), hardware information will be sent to the LTS .

#### Q: How to switch from Soft Binding to Hard Binding and vice versa?

A: There is an API for making the switch. Since [Soft Binding](#soft-binding) is used by default, the following showcases how to switch to [Hard Binding](#hand-binding).

* C

``` c
char errorBuf[512];
DMLTSConnectionParameters paramters;
DBR_InitLTSConnectionParameters(&paramters);
paramters.UUIDGenerationMethod = DM_UUIDGM_HARDWARE;
paramters.handshakeCode = "handshakeCode"; // Please replace the handshakeCode with your own
DBR_InitLicenseFromLTS(&paramters, errorBuf, 512);
```

* C++

``` cpp
int iRet = -1;
char szErrorMsg[256];
DM_LTSConnectionParameters ltspar;    
CBarcodeReader::InitLTSConnectionParameters(&ltspar);
ltspar.UUIDGenerationMethod = DM_UUIDGM_HARDWARE;
ltspar.handshakeCode = "Your-HandshakeCode"; // Please replace the handshakeCode with your own
iRet = CBarcodeReader::InitLicenseFromLTS(&ltspar, szErrorMsg, 256);
if (iRet != DBR_OK)
{
    printf("Error code: %d. Error message: %s\n", iRet, szErrorMsg);
    return -1;
}
```

* C#

``` csharp
DMLTSConnectionParameters ltspar = BarcodeReader.InitLTSConnectionParamters(); 
ltspar.UUIDGenerationMethod = DM_UUIDGM_HARDWARE;          
ltspar.HandshakeCode = "200***001-1000*****"; // Please replace the handshakeCode with your own
EnumErrorCode iRet = BarcodeReader.InitLicenseFromLTS(ltspar, out strErrorMSG);
```

* Java

``` java
DMLTSConnectionParameters ltspar = BarcodeReader.initLTSConnectionParameters();
ltspar.uuidGenerationMethod = DM_UUIDGM_HARDWARE;
ltspar.handshakeCode = "200***001-1000*****"; // Please replace the handshakeCode with your own
ltspar.deploymentType = EnumDMDeploymentType.DM_DT_DESKTOP; // Please replace the deploymentType with your own
BarcodeReader.initLicenseFromLTS(ltspar);
```

* Objective-C for iOS

``` c
iDMLTSConnectionParameters* lts = [[iDMLTSConnectionParameters alloc] init];
lts.handshakeCode = @"handshakeCode"; // Please replace the handshakeCode with your own
lts.UUIDGenerationMethod = DM_UUIDGM_HARDWARE;
_dbr = [[DynamsoftBarcodeReader alloc] initLicenseFromLTS:lts verificationDelegate:self];

* (void)LTSLicenseVerificationCallback:(bool)isSuccess error:(NSError * _Nullable)error

{
NSNumber* boolNumber = [NSNumber numberWithBool:isSuccess];
dispatch_async(dispatch_get_main_queue(), ^{
    [self->m_verificationReceiver performSelector:self->m_verificationCallback withObject:boolNumber withObject:error];

    });
}
```

* Java for Android

``` java
DBRLTSLicenseVerificationListener ltsListener = new DBRLTSLicenseVerificationListener() {
    @Override
    public void LTSLicenseVerificationCallback(boolean success, Exception error) {
        Assert.assertEquals(false, success);
        Assert.assertEquals("ChargeWay for licenseItem is not matched.", error.getMessage());
    }
};
DMLTSConnectionParameters parameters = new DMLTSConnectionParameters();
parameters.uuidGenerationMethod = DM_UUIDGM_HARDWARE;
parameters.handshakeCode = "200***001-1000*****"; // Please replace the handshakeCode with your own
dbr.initLicenseFromLTS(parameters,ltsListener);
```

* Python
```
reader = BarcodeReader()
 connection_paras = reader.init_lts_connection_parameters()
 # Please replace the handshakeCode with your own
 connection_paras.handshake_code = "200***001-1000*****"
 try:
     error = reader.init_licesne_from_lts(connection_paras)
     if error[0] != EnumErrorCode.DBR_OK:
         print(error[1])
 except BarcodeReaderError as bre:
     print(bre)
     ```

