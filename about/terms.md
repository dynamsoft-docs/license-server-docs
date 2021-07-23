---
layout: default-layout
title: Terms involved in Dynamsoft License Server
keywords: Terms, Dynamsoft, License Server, 
description: This page has defintions and descriptions about Dynamsoft License Server Terms
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
| Usage Trackable | No | Optional |
| Hardware binding | Required | Optional |

## Public Trial License

A public trial license is a special license provided by Dynamsoft for all users to test Dynamsoft Products for up to 7 days.

This license is based on License 2.0, therefore, network is required for it to work.

Dynamsoft is gradually rolling out this license in the products. If you are having trouble getting this license to work, please feel free to [contact us](https://www.dynamsoft.com/company/contact/).

## Private Trial License

The old trial license was a string of alphanumeric characters and was not trackable. A private trial license is designed to replace it.

Simply put, a private trial license is a [Per Device]({{site.about}}licensetypes.html#per-device) license good for 30 days and 300 devices and should only be used for product evaluation purposes.

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

Therefore, Dynamsoft invented the concept of a "Handshake Code". An application using a Dynamsoft SDK acquires a local license from Dynamsoft's [Dynamsoft License Server](#dynamsoft-license-server) through a specific Handshake Code.

* The same Handshake Code can be configured to contain permits from different License Items
* The permit from a single License Item can be shared by multiple Handshake Codes

By doing this, the code of your application doesn't need to change, even if different permits are needed at a later date.

A few things to note

* Quota consumption is counted against the License Item in use
* Statistics are summarized both per Handshake Code and per License Item

## Default Handshake Code

For each new organization added to a [Dynamsoft License Server](#dynamsoft-license-server), a default Handshake Code is created. This Handshake Code is used by default when an application only specifies the license by its [Organization ID](#organization-id).

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

### Dynamic Web TWAIN

```javascript
Dynamsoft.DWT.organizationID = "Your-Organization-ID";
Dynamsoft.DWT.handshakeCode = "DynamsoftID-CustomCode";
Dynamsoft.DWT.sessionPassword = "The-Password-You-Set";
Dynamsoft.DWT.Load();
```

### Dynamsoft Barcode Reader

* JavaScript

```javascript
Dynamsoft.DWT.BarcodeReader.organizationID = "Your-Organization-ID";
Dynamsoft.DBR.BarcodeReader.handshakeCode = "DynamsoftID-CustomCode";
Dynamsoft.DBR.BarcodeReader.sessionPassword = "The-Password-You-Set";
let reader = await Dynamsoft.DBR.BarcodeReader.createInstance();
```

* C++

```cpp
int iRet = -1;
char szErrorMsg[256];
DM_DLSConnectionParameters dlspar;    
CBarcodeReader::InitDLSConnectionParameters(&dlspar);
dlspar.organizationID = "Your-Organization-ID";
dlspar.handshakeCode = "Your-HandshakeCode"; // Please replace the handshakeCode with your own
dlspar.SessionPassword = "The-Password-You-Set";
iRet = CBarcodeReader::InitLicenseFromDLS(&dlspar, szErrorMsg, 256);
if (iRet != DBR_OK)
{
    printf("Error code: %d. Error message: %s\n", iRet, szErrorMsg);
    return -1;
}
```

* CSharp

```csharp
DMDLSConnectionParameters dlspar = BarcodeReader.InitDLSConnectionParamters();    
dlspar.OrganizationID = "Your-Organization-ID";       
dlspar.HandshakeCode = "Your-HandshakeCode";
dlspar.SessionPassword = "The-Password-You-Set";
EnumErrorCode iRet = BarcodeReader.InitLicenseFromDLS(dlspar, out strErrorMSG);
```

* Java

```java
DMDLSConnectionParameters dlspar = BarcodeReader.initDLSConnectionParameters();
dlspar.organizationID = "Your-Organization-ID";
dlspar.handshakeCode = "Your-HandshakeCode";
dlspar.sessionPassword = "The-Password-You-Set";
BarcodeReader.initLicenseFromDLS(dlspar);
```

* Java for Android

```java
DBRDLSLicenseVerificationListener dlsListener = new DBRDLSLicenseVerificationListener() {
    @Override
    public void DLSLicenseVerificationCallback(boolean success, Exception error) {
        Assert.assertEquals(false, success);
        Assert.assertEquals("ChargeWay for licenseItem is not matched.", error.getMessage());
    }
};
DMDLSConnectionParameters dlspar = new DMDLSConnectionParameters();
dlspar.organizationID = "Your-Organization-ID";
dlspar.handshakeCode = "Your-HandshakeCode"; // Please replace the handshakeCode with your own
dlspar.sessionPassword = "The-Password-You-Set";
dbr.initLicenseFromDLS(dlspar,dlsListener);
```

* Objective-C for iOS

```c
@interface <DMDLSLicenseVerificationDelegate>

iDMDLSConnectionParameters* dlspar = [[iDMDLSConnectionParameters alloc] init];
dlspar.organizationID = @"Your-Organization-ID";
dlspar.handshakeCode = @"Your-HandshakeCode";
dlspar.sessionPassword = @"The-Password-You-Set";
_dbr = [[DynamsoftBarcodeReader alloc] initLicenseFromDLS:dlspar verificationDelegate:self];

* (void)DLSLicenseVerificationCallback:(bool)isSuccess error:(NSError * _Nullable)error

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

* Swift for iOS

```swift
let dlspar = iDMDLSConnectionParameters();
dlspar.handshakeCode = "*****-hs-****";
dlspar.sessionPassword = "******";
_dbr = DynamsoftBarcodeReader(licenseFromDLS: dlspar, verificationDelegate: self);

func dlsLicenseVerificationCallback(_ isSuccess: Bool, error: Error?)
{
    if isSuccess {
        DispatchQueue.main.async{
            print("ifsuccess : \(isSuccess)");
            print("error code : \(error.code)");
            print("errormsg : \(error.userInfo)");      
        }
    }
}
```

* Python

```python
reader = BarcodeReader()
 connection_paras = reader.init_dls_connection_parameters()
 # Please replace the handshakeCode with your own
 connection_paras.organization_id = "Your-Organization-ID"
 connection_paras.handshake_code = "Your-HandshakeCode"
 connection_paras.session_password = "The-Password-You-Set"
 try:
     error = reader.init_licesne_from_dls(connection_paras)
     if error[0] != EnumErrorCode.DBR_OK:
         print(error[1])
 except BarcodeReaderError as bre:
     print(bre)
```

<!--

* Dynamic Web TWAIN

```javascript
Dynamsoft.WebTwainEnv.SessionPassword = "";
```

-->

## License File

A License File describes one or multiple [License Items](#license-item) and the status of these items.

Each License File has a unique `LicenseId` and an [ `Alias` ](#alias). You can also find out the version of the license scheme, whether the license has been activated, etc. For example

```text
LicenseId: 100028117
Alias: 
LicenseTextVersion: 2.0
CustomerDynamId: 216998
LicenseStatus: Activated
LicenseItems:
...//one or multiple License Items
```

When you place an order, a License File containing all the License Items will automatically be generated. Before the License is activated, you will see the "LicenseStatus" as "new" in the file. Otherwise it will say "Activated".

If you are using a license server hosted by Dynamsoft, the License File is only information about your order for your reference and is not necessary to run the license. However, if you are hosting your own license server, you will need the License File to actually empower the server.

## Deployment Type

The deployment type means how and where the software is being used. For example. The type "mobile" means the software runs in native mobile applications on iOS and Android while the type "browser" means the software runs in web applications within browsers on any operating system. At present, the types are

| Deployment Type | Application Type |
|:-:|:-:|
| Browser | A web application running in browsers |
| Mobile | A native application running on iOS or Android |
| Server (Workstation) | An application running on Windows or Linux that processes requests from other client devices |
| Desktop | An application running on Windows, Linux or macOS that handles requests on this specific device. |
| Embedded | An application running on ARM-based Linux that handles requests on this specific device. |

## Dynamsoft License Server

The Dynamsoft License Server, or DLS for short, is a proprietary software developed by Dynamsoft for license distribution.

Dynamsoft hosts a copy of the software for customers who don't want to trouble themselves with managing the license. However, the software can also be self-hosted. For more information, please see:

* [Self-hosting License Server]({{site.selfhosting}}index.html)
* [Dynamsoft-hosting License Server]({{site.dshosting}}index.html)

## Tolerance Stage

Dynamsoft allows excessive usage of the licenses in case the licensee fails to extend or expand the license in time. For difference license types, this stage means different things:

| License Type | Tolerance Stage |
|:-:|:-:|
| `Per Barcode Scan` | `round(5% * quota)` is allowed after the actual quota runs out. |
| `Per Page` | `round(5% * quota)` is allowed after the actual quota runs out. |
| `Per Device` | `round(10% * quota)` is allowed after the actual quota runs out. |
| `Per Concurrent Device` | A number of exceptions are allowed and the number grows as time passes. |
| `Per Concurrent Instance` | A number of exceptions are allowed and the number grows as time passes. |
| All Types | 7 days are allowed after the license expires. |

## DLS UUID

The UUID here means a unique ID for the machine where DLS is deployed. This UUID will be bound to the license during license activation. After that, this license can only be imported and used on this particular machine. Therefore, make sure this machine assigned for production usage is stable.

You can find the UUID of your DLS on the [admin portal](https://www.dynamsoft.com/license-/docs/selfhosting/managedls.html?ver=latest#log-in-dls-management-portal) once you have successfully installed DLS .

A UUID is bound to one or multiple unique hardware identification labels which include

* ProcessorId
* Media Access Control Address
* Machine ID
* Motherboard Serial Number

If the hardware changes and any of the bound labels is different, the license binding will fail and the license will be unusable. Therefore, be cautious when changing server hardware.

## Client UUID

Each client machine (a device) is also identified by its UUID. This UUID is generated the first time the client machine gets authorized to use a license. All usage reports generated on this client will include this UUID too.

The following table shows the differences between DLS UUID and Client UUID

| | DLS UUID | Client UUID |
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

If you don't mind sharing the device information with the DLS , you can also generate UUID via "Hard Binding".

### Hard Binding

"Hard Binding" means a UUID is directly generated with the collected device information (only for Desktop/Server/Mobile/Embeded editions).

* Desktop/Server/Embeded: the CPU ID and OS ID are collected
* Mobile: the unique device string provided by the device itself is collected

The good news is that as long as you don't change the CPU or reinstall the operating system, a device will always be recognized by the DLS . On the other hand, this means that the DLS can decrypt the UUID to obtain the actual device information.

### Questions

#### Q: Does the UUID give away information about my device?

A: By default, the answer is no because [Soft Binding](#soft-binding) is used. But if you choose to use [Hard Binding](#hand-binding), hardware information will be sent to the DLS .

#### Q: How to switch from Soft Binding to Hard Binding and vice versa?

A: There is an API for making the switch. Since [Soft Binding](#soft-binding) is used by default, the following showcases how to switch to [Hard Binding](#hand-binding).

* C

```c
char errorBuf[512];
DMDLSConnectionParameters paramters;
DBR_InitDLSConnectionParameters(&paramters);
paramters.UUIDGenerationMethod = DM_UUIDGM_HARDWARE;
paramters.handshakeCode = "handshakeCode"; // Please replace the handshakeCode with your own
DBR_InitLicenseFromDLS(&paramters, errorBuf, 512);
```

* C++

```cpp
int iRet = -1;
char szErrorMsg[256];
DM_DLSConnectionParameters dlspar;    
CBarcodeReader::InitDLSConnectionParameters(&dlspar);
dlspar.UUIDGenerationMethod = DM_UUIDGM_HARDWARE;
dlspar.handshakeCode = "Your-HandshakeCode"; // Please replace the handshakeCode with your own
iRet = CBarcodeReader::InitLicenseFromDLS(&dlspar, szErrorMsg, 256);
if (iRet != DBR_OK)
{
    printf("Error code: %d. Error message: %s\n", iRet, szErrorMsg);
    return -1;
}
```

* C#

```csharp
DMDLSConnectionParameters dlspar = BarcodeReader.InitDLSConnectionParamters(); 
dlspar.UUIDGenerationMethod = DM_UUIDGM_HARDWARE;          
dlspar.HandshakeCode = "200***001-1000*****"; // Please replace the handshakeCode with your own
EnumErrorCode iRet = BarcodeReader.InitLicenseFromDLS(dlspar, out strErrorMSG);
```

* Java

```java
DMDLSConnectionParameters dlspar = BarcodeReader.initDLSConnectionParameters();
dlspar.uuidGenerationMethod = DM_UUIDGM_HARDWARE;
dlspar.handshakeCode = "200***001-1000*****"; // Please replace the handshakeCode with your own
dlspar.deploymentType = EnumDMDeploymentType.DM_DT_DESKTOP; // Please replace the deploymentType with your own
BarcodeReader.initLicenseFromDLS(dlspar);
```

* Objective-C for iOS

```c
iDMDLSConnectionParameters* dlspar = [[iDMDLSConnectionParameters alloc] init];
dlspar.handshakeCode = @"handshakeCode"; // Please replace the handshakeCode with your own
dlspar.UUIDGenerationMethod = DM_UUIDGM_HARDWARE;
_dbr = [[DynamsoftBarcodeReader alloc] initLicenseFromDLS:dlspar verificationDelegate:self];

* (void)DLSLicenseVerificationCallback:(bool)isSuccess error:(NSError * _Nullable)error

{
NSNumber* boolNumber = [NSNumber numberWithBool:isSuccess];
dispatch_async(dispatch_get_main_queue(), ^{
    [self->m_verificationReceiver performSelector:self->m_verificationCallback withObject:boolNumber withObject:error];

    });
}
```

* Java for Android

```java
DBRDLSLicenseVerificationListener dlsListener = new DBRDLSLicenseVerificationListener() {
    @Override
    public void DLSLicenseVerificationCallback(boolean success, Exception error) {
        Assert.assertEquals(false, success);
        Assert.assertEquals("ChargeWay for licenseItem is not matched.", error.getMessage());
    }
};
DMDLSConnectionParameters dlspar = new DMDLSConnectionParameters();
dlspar.uuidGenerationMethod = DM_UUIDGM_HARDWARE;
dlspar.handshakeCode = "Your-HandshakeCode"; // Please replace the handshakeCode with your own
dbr.initLicenseFromDLS(dlspar,dlsListener);
```

* Python

```python
reader = BarcodeReader()
 connection_paras = reader.init_dls_connection_parameters()
 # Please replace the handshakeCode with your own
 connection_paras.handshake_code = "Your-HandshakeCode"
 connection_paras.uuid_generation_method = EnumDMUUIDGenerationMethod.DM_UUIDGM_HARDWARE
 try:
     error = reader.init_licesne_from_dls(connection_paras)
     if error[0] != EnumErrorCode.DBR_OK:
         print(error[1])
 except BarcodeReaderError as bre:
     print(bre)
```
