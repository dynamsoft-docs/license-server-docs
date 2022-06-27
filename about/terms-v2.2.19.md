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

License 2.0 is a new generation licensing protocol designed and implemented by Dynamsoft for its products, including Dynamsoft Barcode Reader, Dynamic Web TWAIN, and more.

The following table shows the differences between License 1.0 and 2.0:

| | License 1.0 | License 2.0 |
|:-:|:-:|:-:|
| Expirable | Yes | Yes |
| Usage trackable | No | Optional |
| Hardware binding | Required | Optional |

## Public Trial License

A public trial license is a special license provided by Dynamsoft for all users to test Dynamsoft Products for up to 7 days.

This license is based on License 2.0 and network connection is required for it to work.

Dynamsoft is gradually rolling out this license in the products. If you are having trouble getting this license to work, please feel free to [contact us](https://www.dynamsoft.com/company/contact/).

## Private Trial License

The old trial license was a string of alphanumeric characters and was not trackable. A private trial license is designed to replace it.

Simply put, a private trial license is a [Per Device]({{site.about}}licensetypes.html#per-device) license good for 30 days and 300 devices by default and should only be used for product evaluation purposes.

## Alias

An Alias is another way to identify a license. You can set a meaningful Alias to a license so that you can easily identify the purpose of the license.

A default Alias is created automatically that follows the pattern `DM_{License Id}_Date{Activation Date}`.  A more meaningful Alias could be something like `BarcodeReader_License_For_Dynamsoft_ABC_Project`.

A few things to know about the Alias:

* It can only be changed when the license is new. Once the license is activated, it can no longer be changed.
* The Alias will show up in the [License File](#license-file) as a field.
* A License File can only have one Alias.

## License Item

A License Item contains a permit to use a product. For example, a license item can be described as a "10k-Barcode-Scan package for using Dynamsoft Barcode Reader within Browsers". The license item cannot split. 

## Organization ID

An Organization ID uniquely specifies an organization as the licensee of one or multiple License Item(s).

## Handshake Code

If you have multiple applications or projects for which you want to assign different License Items, you can use Handshake Code.

An application using a Dynamsoft SDK acquires a local license from [Dynamsoft License Server](#dynamsoft-license-server) through a specific Handshake Code. When the need for license permits change in future, you can adjust the handshake configuration on the license server side and there is no need to update your application code.

* One Handshake Code can contain permits of multiple License Items
* Multiple Handshake Codes can share the permit of one single License Item 

A few things to note:

* Quota consumption is counted against the License Item in use.
* Statistics are summarized both per Handshake Code and per License Item.

## Default Handshake Code

For each new organization added to a [Dynamsoft License Server](#dynamsoft-license-server), a default Handshake Code is created. This Default Handshake Code is used when an application connects to Dynamsoft License Server with [Organization ID](#organization-id) and no HandShake Code specified.

## Validation Field

A Handshake Code is a string that is set in your code. It is important to secure the Handshake Code and ensure it won't be used by any other parties. For that, the Handshake Code comes with a security setting called **Validation Field**.

A Validation Field is a static characteristic of your application, i.e., Once set, it cannot be changed. At present, the following three Validation Fields are supported:

* Website Domain

> Applicable to Dynamsoft Barcode Reader JavaScript Edition, Dynamic Web TWAIN

* Application ID

> Applicable to Dynamsoft Barcode Reader Mobile Edition

* Process Name

> Applicable to Dynamsoft Barcode Reader desktop and server Editions (C, C++, DotNet, Java, Python, etc.); Dynamsoft Barcode Reader Embedded Edition

## Session Password

The Session Password is another way to protect your license. Unlike the Validation Field, which is essentially validating a characteristic of your application, the Session Password is a simpler and more flexible string that you can set in your application. 

To verify the password, all products have a similar API. For example:

### Dynamic Web TWAIN

```javascript
Dynamsoft.DWT.organizationID = "Your-Organization-ID";
// Dynamsoft.DWT.handshakeCode = "DynamsoftID-CustomCode"; // Optional
Dynamsoft.DWT.sessionPassword = "The-Password-You-Set";
Dynamsoft.DWT.Load();
```

### Dynamsoft Barcode Reader

* JavaScript

```javascript
Dynamsoft.DBR.BarcodeReader.organizationID = "Your-Organization-ID";
// Dynamsoft.DBR.BarcodeReader.handshakeCode = "DynamsoftID-CustomCode"; // Optional
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
// dlspar.handshakeCode = "Your-HandshakeCode"; // Optional
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
// dlspar.HandshakeCode = "Your-HandshakeCode"; // Optional
dlspar.SessionPassword = "The-Password-You-Set";
EnumErrorCode iRet = BarcodeReader.InitLicenseFromDLS(dlspar, out strErrorMSG);
```

* Java

```java
DMDLSConnectionParameters dlspar = BarcodeReader.initDLSConnectionParameters();
dlspar.organizationID = "Your-Organization-ID";
// dlspar.handshakeCode = "Your-HandshakeCode"; // Optional
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
// dlspar.handshakeCode = "Your-HandshakeCode"; // Optional
dlspar.sessionPassword = "The-Password-You-Set";
dbr.initLicenseFromDLS(dlspar,dlsListener);
```

* Objective-C for iOS

```c
@interface <DMDLSLicenseVerificationDelegate>

iDMDLSConnectionParameters* dlspar = [[iDMDLSConnectionParameters alloc] init];
dlspar.organizationID = @"Your-Organization-ID";
// dlspar.handshakeCode = @"Your-HandshakeCode"; // Optional
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
// dlspar.handshakeCode = "*****-hs-****"; // Optional
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
 connection_paras.organization_id = "Your-Organization-ID"
 # handshake_code is optional
 # connection_paras.handshake_code = "Your-HandshakeCode"
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

Each License File has a unique `LicenseId` and an [`Alias`](#alias). You can also find out information like the version of the license scheme, whether the license has been activated, etc. For example:

```text
LicenseId: 100028117
Alias: 
LicenseTextVersion: 2.0
CustomerDynamId: 216998
LicenseStatus: Activated
LicenseItems:
...//one or multiple License Items
```

When you place an order, a License File containing all the License Items will be generated automatically. Before the License is activated, you will see the "LicenseStatus" as "New" in the file; Otherwise it will say "Activated".

If you are using a license server hosted by Dynamsoft, the License File is only for your reference with the information of your order and is not necessary to run the license. However, if you are hosting your own license server, you will need the License File to actually empower the server. See [Dynamsoft License Server](#dynamsoft-license-server) to learn more.

## Deployment Type

The Deployment Type means how and where the application with Dynamsoft's SDK is used. For example, the type "mobile" means the application runs in native mobile devices such as iOS or Android; while the type "browser" means the application runs in browsers on any operating system. At present, the types include:

| Deployment Type | Application Type |
|:-:|:-:|
| Browser | A web application running in browsers |
| Mobile | A native application running on iOS or Android |
| Server (Workstation) | An application running on Windows or Linux that processes requests from other client devices |
| Desktop | An application running on Windows, Linux or macOS that handles requests on this specific device. |
| Embedded | An application running on ARM-based Linux that handles requests on this specific device. |

## Dynamsoft License Server

The Dynamsoft License Server (DLS), is a proprietary software developed by Dynamsoft for license distribution.

Dynamsoft provides both Dynamsoft-hosting and self-hosting options of DLS. For more information, please see:

* [Self-hosting License Server]({{site.selfhosting}}index.html)
* [Dynamsoft-hosting License Server]({{site.dshosting}}index.html)

## Grace Stage

Dynamsoft provides a grace stage in case the licensee fails to extend or expand the license in time. For difference license types:

| License Type | Grace Stage |
|:-:|:-:|
| Per Barcode Scan | `round(5% * quota)` is allowed after the actual quota runs out. |
| Per Page | `round(5% * quota)` is allowed after the actual quota runs out. |
| Per Device | `round(10% * quota)` is allowed after the actual quota runs out. |
| Per Concurrent Device | A number of exceptions are allowed and the number grows as time passes. |
| Per Concurrent Instance | A number of exceptions are allowed and the number grows as time passes. |
| All Types | 7 days are allowed after the license expires. |

## DLS UUID

The UUID here means a unique ID for the machine where DLS is deployed. This UUID will be bound to the license during license activation. After that, this license can only be imported and used on this particular machine. 

After installing DLS, you can find the UUID of your DLS in the [admin portal](https://www.dynamsoft.com/license-/docs/selfhosting/managedls.html?ver=latest#log-in-dls-management-portal) .

A UUID is bound to one or multiple unique hardware identification labels which include:

* ProcessorId
* Media Access Control Address
* Machine ID
* Motherboard Serial Number

If the hardware or any of the bound labels change, the license binding might fail and become unusable. Therefore, be cautious when changing server hardware.

## Client UUID

Each client machine (a device) is also identified by its UUID which is generated the first time a client machine gets authorized to use a license. All usage reports generated on this client will include this UUID.

The following table shows the differences between DLS UUID and Client UUID:

| | DLS UUID | Client UUID |
|:-:|:-:|:-:|
| Bound to the License | Yes | No |
| Bound to usage reports | No | Yes |
| Hardware binding | Required | Optional |

For each device, a Client UUID is generated which is used to uniquely identify the device. In other words, we use UUIDs to count the number of devices supported by a license.

### Generate a UUID

Different mechanism are used for UUID generation for different product editions.

* JavaScript Edition: The UUID is a random string generated when the SDK is first used. The UUID is cached in the browser's indexedDB which represents a specific browser on a certain domain.

  > NOTE:
  >
  > * Multiple browsers on the same device are counted as multiple devices since there will be a UUID generated for each browser.
  > * The same browser accessing multiple websites with different domains is counted separately per domain.

* Mobile Edition:
  * on iOS: The UUID is a random string stored in the keychain associated with the developer's vendor ID (IDFV) and the application ID.
  * on Android: The UUID is a combination of a random string and information about the OS which is either the Android SERIAL number (before Android v8.0) or ANDROID_ID (Android v8.0+). The UUID is saved as part of the application data.

* Other Editions: The UUID is a combination of a random string and information about the device including one or more of the following: CPU ID, OS ID and MAC Addresses. The UUID is saved on the machine in a system directory.

#### Soft Binding

As mentioned above, UUIDs usually contain random information and will be different each time they are generated, even if they are generated on/in the same device/browser. In order to maintain the consistency of the information, so that the same device/browser will not be counted multiple times, the generated UUID will be temporarily stored for later retrieval.

This mechanism is called Soft Binding at Dynamsoft. In contrast, there is another mechanism called Hard Binding, which is only used for SDKs running in a desktop, embedded or server environment.

#### Hard Binding

When using Hard Binding, a UUID is directly generated with information about the device:

* If the device uses an ARM processor, it's based on the OS ID and the MAC Addresses;
* In other cases, it's based on the OS ID and the CPU ID.

With hard binding, the UUID is not saved because the same information can be gathered to regenerate the exact same UUID. However, if you do replace the CPU (or network adapter) or reinstall the operating system, the device will be considered new.

> Note
>
> * When generating a UUID, part of the gathered device information is ignored in the encryption. Therefore the actual device information is never shared with DLS.

### Questions

#### Q: Does the UUID give away information about my device?

A: No. Check out [Client UUID](#client-uuid) for more information.

#### Q: How to switch to Hard Binding?

A: To switch to Hard Binding, you need to configure your project to specify that it will use Hard Binding which will be reflected in a changed License Key. Replace the old key with the updated key to finish the switching.

> NOTE: Previously, for Dynamsoft Barcode Reader, there was an API `UUIDGenerationMethod` for making the switch. The following code snippets show how to switch to [Hard Binding](#hard-binding).
>
> * Python
>
> ```python
>  reader = BarcodeReader()
>  connection_paras = reader.init_dls_connection_parameters()
>  # Please replace the handshakeCode with your own
>  connection_paras.handshake_code = "Your-HandshakeCode"
>  connection_paras.uuid_generation_method = EnumDMUUIDGenerationMethod.DM_UUIDGM_HARDWARE
>  try:
>      error = reader.init_licesne_from_dls(connection_paras)
>      if error[0] != EnumErrorCode.DBR_OK:
>          print(error[1])
>  except BarcodeReaderError as bre:
>      print(bre)
> ```
>
> * C#
>
> ```csharp
> DMDLSConnectionParameters dlspar = BarcodeReader.InitDLSConnectionParamters(); 
> dlspar.UUIDGenerationMethod = DM_UUIDGM_HARDWARE;          
> dlspar.HandshakeCode = "200***001-1000*****"; > Please replace the handshakeCode with your own
> EnumErrorCode iRet = BarcodeReader.InitLicenseFromDLS(dlspar, out strErrorMSG);
> ```
>
> * Java
>
> ```java
> DMDLSConnectionParameters dlspar = BarcodeReader.initDLSConnectionParameters();
> dlspar.uuidGenerationMethod = DM_UUIDGM_HARDWARE;
> dlspar.handshakeCode = "200***001-1000*****"; > Please replace the handshakeCode with your own
> dlspar.deploymentType = EnumDMDeploymentType.DM_DT_DESKTOP; > Please replace the deploymentType with your own
> BarcodeReader.initLicenseFromDLS(dlspar);
> ```
>
> * C++
>
> ```cpp
> int iRet = -1;
> char szErrorMsg[256];
> DM_DLSConnectionParameters dlspar;    
> CBarcodeReader::InitDLSConnectionParameters(&dlspar);
> dlspar.UUIDGenerationMethod = DM_UUIDGM_HARDWARE;
> dlspar.handshakeCode = "Your-HandshakeCode"; > Please replace the handshakeCode with your own
> iRet = CBarcodeReader::InitLicenseFromDLS(&dlspar, szErrorMsg, 256);
> if (iRet != DBR_OK)
> {
>     printf("Error code: %d. Error message: %s\n", iRet, szErrorMsg);
>     return -1;
> }
> ```
>
> * C
>
> ```c
> char errorBuf[512];
> DMDLSConnectionParameters paramters;
> DBR_InitDLSConnectionParameters(&paramters);
> paramters.UUIDGenerationMethod = DM_UUIDGM_HARDWARE;
> paramters.handshakeCode = "handshakeCode"; // Please replace the handshakeCode with your own
> DBR_InitLicenseFromDLS(&paramters, errorBuf, 512);
> ```
