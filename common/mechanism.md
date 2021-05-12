---
layout: default-layout
title: How trackable licenses work
keywords: license tracking, mechanism
description: This page describes how license tracking is done
breadcrumbText: Mechanism
needAutoGenerateSidebar: true
---

# How trackable licenses work

> Important NOTE
> 
> The following content assumes that you have already activated your license, if you haven't, please first [activate it]({{site.about}}activate.html).

All Dynamsoft SDKs that support trackable licenses have a built-in mechanism to get authorization at initialization as well as collect and report its usage during runtime. This article is about how to use such a trackable license.

NOTE: If you are using an old browser like IE 9 to access a web application, please also check out [Special Notice for IE 9](#special-notice-for-ie-9).

## Configure LTS

> Read more on [what is LTS]({{site.about}}terms.html#license-tracking-server)

The following code snippets show how to configure LTS. If you are using Dynamsoft-Hosting LTS , you can skip this step.

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
DM_LTSConnectionParameters ltspar;    
CBarcodeReader::InitLTSConnectionParameters(&ltspar);
ltspar.mainServerURL = "https://your.mainServer.com"; // Please replace the server URL with your own
iRet = CBarcodeReader::InitLicenseFromLTS(&ltspar, szErrorMsg, 256);
```

* CSharp

``` csharp
// DBR
DMLTSConnectionParameters ltspar = BarcodeReader.InitLTSConnectionParamters();           
ltspar.MainServerURL = "https://your.mainServer.com";
```

* Java

``` java
// DBR
DMLTSConnectionParameters ltspar = BarcodeReader.initLTSConnectionParameters();
ltspar.mainServerURL = "https://your.mainServer.com";
```

* Python

``` python
// DBR
br = BarcodeReader();
ltspar = reader.init_lts_connection_parameters();
ltspar.mainServerURL = "https://your.mainServer.com";
```

On Android

``` java
// DBR
DBRLTSLicenseVerificationListener ltsListener = new DBRLTSLicenseVerificationListener() {
    @Override
    public void LTSLicenseVerificationCallback(boolean success, Exception error) {
        Assert.assertEquals(false, success);
        Assert.assertEquals("ChargeWay for licenseItem is not matched.", error.getMessage());
    }
};
DMLTSConnectionParameters parameters = new DMLTSConnectionParameters();
parameters.mainServerURL = "https://your.mainServer.com";
```

On iOS

``` c
// DBR
iDMLTSConnectionParameters* lts = [[iDMLTSConnectionParameters alloc] init];
lts.mainServerURL = @"https://your.mainServer.com";
```

## Specify the Organization ID

> Read more on [what is an Organization ID]({{site.about}}terms.html#organization-id)

You can acquire the license from LTS by specifying your Organization ID. At present, this is supported in the Android and iOS editions of Dynamsoft Barcode Reader.

On Android

``` java
// DBR
DBRLTSLicenseVerificationListener ltsListener = new DBRLTSLicenseVerificationListener() {
    @Override
    public void LTSLicenseVerificationCallback(boolean success, Exception error) {
        Assert.assertEquals(false, success);
        Assert.assertEquals("ChargeWay for licenseItem is not matched.", error.getMessage());
    }
};
DMLTSConnectionParameters parameters = new DMLTSConnectionParameters();
parameters.organizationId = "Your-OrganizationId";
dbr.initLicenseFromLTS(parameters,ltsListener);
```

On iOS

``` c
// DBR
iDMLTSConnectionParameters* lts = [[iDMLTSConnectionParameters alloc] init];
lts.organizationId = @"Your-OrganizationId";
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

## Specify the Handshake Code

> Read more on [what is Handshake Code]({{site.about}}terms.html#handshake-code)

* JavaScript

``` javascript
// DBR
Dynamsoft.DBR.BarcodeReader.handshakeCode = "DynamsoftID-CustomCode";
let reader = await Dynamsoft.DBR.BarcodeReader.createInstance();

// DWT
Dynamsoft.DWT.handshakeCode = "DynamsoftID-CustomCode";
Dynamsoft.DWT.Load();
```

For Dynamsoft Barcode Reader JavaScript Edition, the Handshake Code can also be set in the script tag as `data-productKeys` as shown below

``` html
<script src="https://cdn.jsdelivr.net/npm/dynamsoft-javascript-barcode@8/dist/dbr.js" data-productKeys="DynamsoftID-CustomCode"></script>
```

* C++

``` cpp
// DBR
int iRet = -1;
char szErrorMsg[256];
DM_LTSConnectionParameters ltspar;    
CBarcodeReader::InitLTSConnectionParameters(&ltspar);
ltspar.handshakeCode = "Your-HandshakeCode"; // Please replace the handshakeCode with your own
iRet = CBarcodeReader::InitLicenseFromLTS(&ltspar, szErrorMsg, 256);
if (iRet != DBR_OK)
{
    printf("Error code: %d. Error message: %s\n", iRet, szErrorMsg);
    return -1;
}
```

* CSharp

``` csharp
// DBR
DMLTSConnectionParameters ltspar = BarcodeReader.InitLTSConnectionParamters();           
ltspar.HandshakeCode = "Your-HandshakeCode";
EnumErrorCode iRet = BarcodeReader.InitLicenseFromLTS(ltspar, out strErrorMSG);
```

* Java

``` java
// DBR
DMLTSConnectionParameters ltspar = BarcodeReader.initLTSConnectionParameters();
ltspar.handshakeCode = "Your-HandshakeCode";
BarcodeReader.initLicenseFromLTS(ltspar);
```

* Python

``` python
// DBR
reader = BarcodeReader();
ltspar = reader.init_lts_connection_parameters();
ltspar.handshakeCode = "Your-HandshakeCode";
iRet = reader.init_license_from_lts(ltspar);
```

On Android

``` java
// DBR
DBRLTSLicenseVerificationListener ltsListener = new DBRLTSLicenseVerificationListener() {
    @Override
    public void LTSLicenseVerificationCallback(boolean success, Exception error) {
        Assert.assertEquals(false, success);
        Assert.assertEquals("ChargeWay for licenseItem is not matched.", error.getMessage());
    }
};
DMLTSConnectionParameters parameters = new DMLTSConnectionParameters();
parameters.handshakeCode = "Your-HandshakeCode";
dbr.initLicenseFromLTS(parameters,ltsListener);
```

On iOS

``` c
// DBR
iDMLTSConnectionParameters* lts = [[iDMLTSConnectionParameters alloc] init];
lts.handshakeCode = @"Your-HandshakeCode";
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

## Authorization

During initialization, Dynamsoft SDKs connect to LTS to get authorized. The process is simplified as follows

* The SDK sends a request to LTS.
* LTS extracts the Handshake Code from the request and checks its status in the database.
* If the Code exists and its quota is not used up,  LTS returns the authorization.
* Otherwise, a failure message is returned.

### About the request

The request includes the [Client UUID]({{site.about}}terms.html#client-uuid) and the Handshake Code among other information. The Handshake Code is fetched from [your code](#configure-the-handshake-code) and the UUID is fetched from the local cache. If the UUID is not found in the cache, a new one is generated.

### Handle authorization error

For better user experience, you need to handle the authorization error should it happens. The following sample assumes JavaScript is used:

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

When a Dynamsoft SDK uses a trackable license, it will record every successful operation that needs to be trackable. Then it generates a minimum report for each 3-minute time slot and sumbits the report every 3 minutes. We'll dive deeper into the mechanism below.

### Usage report

#### Dynamic Web TWAIN

Dynamic Web TWAIN is used to scan documents or load existing documents for further operations, etc., its usage report includes fields such as

* Time label (indicates which 3-minute slot it covers)
* Handshake Code
* Client UUID
* Count of total processed pages
* Type of importing operations (whether the pages are scanned, captured, etc.)

#### Dynamsoft Barcode Reader

The main purpose of the Barcode Reader is to locate and decode barcodes, therefore, its usage is about successful barcode scans and its report includes fields such as

* Time label (indicates which 3-minute slot it covers)
* Handshake Code
* Client UUID
* Count of barcodes
* Type of barcodes

### Time

* 3-minute for reports

  Dynamsoft uses absolute time when generating usage reports. This means, each time slot is fixed, for example, the first time slot of the day is always 00:00:00 ~ 00:03:00 and the second is 00:03:00 ~ 00:06:00 and so on. Each successful operation (like a barcode scan) has a time stamp of its own and is counted in the 3-minute window in which it is done.

* 3-minute for submitting reports

  Unlike the time used for report generating which must be precise, report submitting needs to be done timely. Therefore, the moment the SDK finishes initialization, it'll check whether there are usage reports left unsubmitted and submit them if any. After that, it'll submit new report (if any) every 3 minutes.

### Report submission

Dynamsoft SDKs submit usage reports to LTS with HTTP Post requests. If the submission succeeds, it'll remove the local copy of the report, otherwise, the report remains on the device and will be submitted again the next time the SDK initializes. Note that the SDK won't attempt to submit failed reports during the same session.

If a report is not submitted, it'll be kept on the client for up to 30 days after which it'll be purged.

### Report analysis

LTS receives usage reports from client devices, count the usage against certain license items, and then does the math to make overall usage reports. These reports are done per each Handshake Code and per License Item. Read more on [statistics page]({{site.common}}statistics.html).

## Special Notice for IE 9

For IE 9, in order to use the license, you must make sure of two things

* The option `Access data sources across domains` must be set to `Enabled` in "Security Settings"
* The [License Server URL](#configure-lts) and your own web site URL must both be included in "Trusted Sites"
