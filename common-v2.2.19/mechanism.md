---
layout: default-layout
title: How trackable licenses work
keywords: license tracking, mechanism
description: This page describes how license tracking is done
breadcrumbText: Mechanism
needAutoGenerateSidebar: true
noTitleIndex: true
---

# How trackable licenses work

> NOTE:
> 
> The following content assumes that you have already activated your license. If you haven't, please first [activate it]({{site.about}}activate.html).

All Dynamsoft SDKs that support trackable licenses have a built-in mechanism for getting authorization at initialization as well as collecting and reporting license usage during runtime. This article is about how to use such a trackable license.

Currently supported products:

* Dynamic Web TWAIN (v17.1+)
* Dynamsoft Barcode Reader (JavaScript, Android and iOS Editions, v8.2.5+)
* Dynamsoft Label Recognition (Android and iOS Editions)
* Dynamsoft Camera Enhancer (Android and iOS Editions)

The license system shall work fine in all mainstream browsers. However, if you are using an old browser like **IE 9**, please make sure to:

* set the option "Access data sources across domains" under "Security Settings" to "Enabled"
* set the [License Server URL](#configure-dls) and your own web site URL as "Trusted Sites"

## Configure DLS

> Read more on [what is DLS]({{site.about}}terms.html#dynamsoft-license-server)

If you are using Dynamsoft-Hosting DLS, you can skip this step. The following code snippets show how to configure connecting to your **self-hosting DLS**.  

* JavaScript

``` javascript
// DBR 
Dynamsoft.DBR.BarcodeReader.licenseServer = ["https://your.mainServer.com"];
// DWT
Dynamsoft.DWT.licenseServer = ["https://your.mainServer.com"];
```

* C++

``` cpp
// DBR
int iRet = -1;
char szErrorMsg[256];
DM_DLSConnectionParameters dlspar;    
CBarcodeReader::InitDLSConnectionParameters(&dlspar);
dlspar.mainServerURL = "https://your.mainServer.com"; // Please replace the server URL with your own
iRet = CBarcodeReader::InitLicenseFromDLS(&dlspar, szErrorMsg, 256);
```

* CSharp

``` csharp
// DBR
DMDLSConnectionParameters dlspar = BarcodeReader.InitDLSConnectionParamters();           
dlspar.MainServerURL = "https://your.mainServer.com";
```

* Java

``` java
// DBR
DMDLSConnectionParameters dlspar = BarcodeReader.initDLSConnectionParameters();
dlspar.mainServerURL = "https://your.mainServer.com";
```

* Python

``` python
// DBR
br = BarcodeReader();
dlspar = reader.init_dls_connection_parameters();
dlspar.main_server_url = "https://your.mainServer.com";
```

* On Android

``` java
// DBR
DBRDLSLicenseVerificationListener dlsListener = new DBRDLSLicenseVerificationListener() {
    @Override
    public void DLSLicenseVerificationCallback(boolean success, Exception error) {
        Assert.assertEquals(false, success);
        Assert.assertEquals("ChargeWay for licenseItem is not matched.", error.getMessage());
    }
};
DMDLSConnectionParameters parameters = new DMDLSConnectionParameters();
parameters.mainServerURL = "https://your.mainServer.com";
```

* On iOS

``` c
// DBR
iDMDLSConnectionParameters* dls = [[iDMDLSConnectionParameters alloc] init];
dls.mainServerURL = @"https://your.mainServer.com";
```

## How to set the license

You can set the license either by specifying the Organization ID or Handshake Code

During initialization, Dynamsoft SDKs connect to DLS to get authorized. The process is as follows:

* The SDK sends a request to DLS. 

  The request includes the [Client UUID]({{site.about}}terms.html#client-uuid) and the [Handshake Code]({{site.about}}terms.html#handshake-code) among other information. The Handshake Code is fetched from [your code](#configure-the-handshake-code) and the UUID is fetched from the local cache. If the UUID is not found in the cache, a new one is generated.
* DLS extracts the [Handshake Code]({{site.about}}terms.html#handshake-code) from the request and checks its status in the database.
* If the Handshake Code exists and its quota is not used up, DLS returns the authorization; Otherwise, DLS returns a failure message.

To get authorization, you can mainly use Organization ID and Handshake Code (optional). 

### Specify the Organization ID

> Read more on [what is an Organization ID]({{site.about}}terms.html#organization-id)

You can get license authorization from DLS by specifying your Organization ID. Each Organization ID comes with a default [Handshake code]({{site.about}}terms.html#handshake-code).

Check out the code snippets:

* JavaScript

``` javascript
// DBR for JavaScript
Dynamsoft.DBR.BarcodeReader.organizationID = "YOUR-ORGANIZATION-ID";
let reader = await Dynamsoft.DBR.BarcodeReader.createInstance();
// DWT
Dynamsoft.DWT.organizationID = "YOUR-ORGANIZATION-ID";
Dynamsoft.DWT.Load();
```

> NOTE:
> 
> If you are using a long product key with the API `productKeys` as shown below, you can replace it with `organizationID` once you get your own Organization ID. Although both licensing ways are supported, they cannot be used together.

> ```javascript
> Dynamsoft.DBR.BarcodeReader.productKeys = "t0069oQAAAAWAfpGnxxsFYz....."; // The traditional product key
> ```

* Android

``` java
DBRDLSLicenseVerificationListener dlsListener = new DBRDLSLicenseVerificationListener() {
    @Override
    public void DLSLicenseVerificationCallback(boolean success, Exception error) {
        Assert.assertEquals(false, success);
        Assert.assertEquals("ChargeWay for licenseItem is not matched.", error.getMessage());
    }
};
DMDLSConnectionParameters parameters = new DMDLSConnectionParameters();
parameters.organizationId = "123456"; // replace the number 123456 with YOUR-ORGANIZATION-ID
dbr.initLicenseFromDLS(parameters,dlsListener);
```

* iOS

``` c
iDMDLSConnectionParameters* dls = [[iDMDLSConnectionParameters alloc] init];
dls.organizationId = @"123456"; // replace the number 123456 with YOUR-ORGANIZATION-ID
_dbr = [[DynamsoftBarcodeReader alloc] initLicenseFromDLS:dls verificationDelegate:self];

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

### Specify the Handshake Code

> Read more on [what is Handshake Code]({{site.about}}terms.html#handshake-code)

Usually it's enough to use Organization ID, which comes with a default Handshake code, for you to get license authorization from DLS. However, if you have configured multiple Handshake Code for differentiating license usage among different projects in license portal, you can specify the Handshake Code correspondingly in your application like below.

* JavaScript

``` javascript
// DBR
Dynamsoft.DBR.BarcodeReader.handshakeCode = "DynamsoftID-CustomCode";
let reader = await Dynamsoft.DBR.BarcodeReader.createInstance();

// DWT
Dynamsoft.DWT.handshakeCode = "DynamsoftID-CustomCode";
Dynamsoft.DWT.Load();
```

For Dynamsoft Barcode Reader JavaScript Edition, the Handshake Code can also be set in the script tag as `data-productKeys` as shown below:

``` html
<script src="https://cdn.jsdelivr.net/npm/dynamsoft-javascript-barcode@8/dist/dbr.js" data-productKeys="DynamsoftID-CustomCode"></script>
```

* C++

``` cpp
// DBR
int iRet = -1;
char szErrorMsg[256];
DM_DLSConnectionParameters dlspar;    
CBarcodeReader::InitDLSConnectionParameters(&dlspar);
dlspar.handshakeCode = "Your-HandshakeCode"; // Please replace the handshakeCode with your own
iRet = CBarcodeReader::InitLicenseFromDLS(&dlspar, szErrorMsg, 256);
if (iRet != DBR_OK)
{
    printf("Error code: %d. Error message: %s\n", iRet, szErrorMsg);
    return -1;
}
```

* CSharp

``` csharp
// DBR
DMDLSConnectionParameters dlspar = BarcodeReader.InitDLSConnectionParamters();           
dlspar.HandshakeCode = "Your-HandshakeCode";
EnumErrorCode iRet = BarcodeReader.InitLicenseFromDLS(dlspar, out strErrorMSG);
```

* Java

``` java
// DBR
DMDLSConnectionParameters dlspar = BarcodeReader.initDLSConnectionParameters();
dlspar.handshakeCode = "Your-HandshakeCode";
BarcodeReader.initLicenseFromDLS(dlspar);
```

* Python

``` python
// DBR
reader = BarcodeReader();
dlspar = reader.init_dls_connection_parameters();
dlspar.handshake_code = "Your-HandshakeCode";
iRet = reader.init_license_from_dls(dlspar);
```

* On Android

``` java
// DBR
DBRDLSLicenseVerificationListener dlsListener = new DBRDLSLicenseVerificationListener() {
    @Override
    public void DLSLicenseVerificationCallback(boolean success, Exception error) {
        Assert.assertEquals(false, success);
        Assert.assertEquals("ChargeWay for licenseItem is not matched.", error.getMessage());
    }
};
DMDLSConnectionParameters parameters = new DMDLSConnectionParameters();
parameters.handshakeCode = "Your-HandshakeCode";
dbr.initLicenseFromDLS(parameters,dlsListener);
```

* On iOS

``` c
// DBR
iDMDLSConnectionParameters* dls = [[iDMDLSConnectionParameters alloc] init];
dls.handshakeCode = @"Your-HandshakeCode";
_dbr = [[DynamsoftBarcodeReader alloc] initLicenseFromDLS:dls verificationDelegate:self];

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

### Handle authorization error

For better user experience, it's suggested to handle the authorization error should it happens, e.g. for JavaScript:

``` javascript
try {
    reader = await Dynamsoft.DBR.BarcodeReader.createInstance();
} catch (ex) {
    // Check the error message and if it's a license error, like
    // "License has exceeded its limit."
    // Try to notify the user to try again or to contact the site administrator
}
```

## License Tracking

When a Dynamsoft SDK uses a trackable license, every successful operation that needs to be tracked will be recorded, then DLS generates a minimum report for each 3-minute time slot and sumbits the report every 3 minutes. We'll dive deeper into the mechanism below.

### Usage report

A license usage report includes the meaningful data for tracking license usage. For example:

#### Dynamic Web TWAIN

Dynamic Web TWAIN is used to scan documents or load existing documents for further operations. So its usage report includes fields such as

* Time label (indicates which 3-minute slot it covers)
* Handshake Code
* Client UUID
* Count of total processed pages
* Type of importing operations (whether the pages are scanned, imported, etc.)

#### Dynamsoft Barcode Reader

Dynamsoft Barcode Reader is mainly used for decoding barcodes. Therefore, its usage is about successful barcode scans and its report includes fields such as

* Time label (indicates which 3-minute slot it covers)
* Handshake Code
* Client UUID
* Count of barcodes
* Type of barcodes

### Time

* 3-minute for reports

  Dynamsoft uses absolute time when generating usage reports. This means, each time slot is fixed, for example, the first time slot of the day is always 00:00:00 ~ 00:03:00 and the second is 00:03:00 ~ 00:06:00 and so on. Each successful operation (like a barcode scan) has a time stamp of its own and is counted in the 3-minute window in which it is done.

* 3-minute for submitting reports

  License usage report are submitted timely. The moment the SDK finishes initialization, it'll
  * check whether there are usage reports left unsubmitted and submit them right away if any. 
  * submit new report (if any) every 3 minutes.

### Report submission

Dynamsoft SDKs submit usage reports to DLS with HTTP Post requests. If the submission succeeds, the local copy of the report will be removed; otherwise, the report remains on the device (kept up to 30 days before purging) and will be submitted again the next time the SDK initializes. The SDK won't attempt to submit failed reports during the same session.

### Report analysis

DLS receives usage reports from client devices, count the usage against certain license items, and then does the math to make overall usage reports. These reports are done per each Handshake Code and per License Item. Read more on [statistics page]({{site.common}}statistics.html).
